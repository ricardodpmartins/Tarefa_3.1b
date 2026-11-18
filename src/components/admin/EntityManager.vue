<template>
  <main class="page-section">
    <b-container>
      <HeaderPage :title="title" />
      <p class="text-center">{{ description }}</p>

      <div class="mb-4">
        <router-link
          :to="{ name: 'admin' }"
          class="btn btn-outline-secondary mr-2"
        >
          Voltar à administração
        </router-link>
        <button class="btn btn-success" @click="add">
          Adicionar registo
        </button>
      </div>

      <div v-if="selected" class="card mb-4">
        <div class="card-header">Detalhes</div>
        <div class="card-body">
          <p v-for="field in fields" :key="field.key">
            <strong>{{ field.label }}:</strong>
            {{ displayValue(field, selected) }}
          </p>
          <button class="btn btn-outline-secondary" @click="selected = null">
            Fechar
          </button>
        </div>
      </div>

      <div v-if="editing" class="card mb-4">
        <div class="card-header">
          {{ editId === null ? "Adicionar" : "Editar" }}
          {{ singular }}
        </div>
        <div class="card-body">
          <form @submit.prevent="save">
            <div v-for="field in fields" :key="field.key" class="form-group">
              <label :for="entityKey + field.key">
                {{ field.label }}
              </label>
              <select
                v-if="field.options"
                :id="entityKey + field.key"
                v-model="form[field.key]"
                class="form-control"
                :required="field.required !== false"
              >
                <option value="" disabled>Seleciona uma opção</option>
                <option v-if="isLegacyOption(field)" :value="form[field.key]">
                  {{ form[field.key] }} (valor anterior)
                </option>
                <option
                  v-for="option in field.options"
                  :key="option.value"
                  :value="option.value"
                >
                  {{ option.label }}
                </option>
              </select>
              <input
                v-else
                :id="entityKey + field.key"
                v-model.trim="form[field.key]"
                class="form-control"
                :type="field.type || 'text'"
                :required="field.required !== false"
                maxlength="150"
              />
            </div>
            <button type="submit" class="btn btn-success mr-2">
              Guardar
            </button>
            <button
              type="button"
              class="btn btn-outline-secondary"
              @click="cancel"
            >
              Cancelar
            </button>
          </form>
        </div>
      </div>

      <!-- Vista mobile: cartoes em vez de tabela -->
      <div class="mobile-entity-list d-md-none mb-4">
        <div v-if="items.length === 0" class="alert alert-info">
          Não existem registos.
        </div>

        <div v-for="item in items" :key="item.id" class="card mb-3">
          <div class="card-header font-weight-bold">
            {{ item[fields[0].key] }}
          </div>

          <div class="card-body">
            <dl class="mb-3">
              <template v-for="field in fields">
                <dt :key="field.key + '-label'" class="small">
                  {{ field.label }}
                </dt>
                <dd :key="field.key + '-value'">
                  {{ displayValue(field, item) }}
                </dd>
              </template>
            </dl>

            <div class="d-flex flex-wrap">
              <button
                type="button"
                class="btn btn-sm btn-outline-info mr-2 mb-2"
                @click="selected = item"
              >
                Ver
              </button>

              <button
                type="button"
                class="btn btn-sm btn-outline-primary mr-2 mb-2"
                @click="edit(item)"
              >
                Editar
              </button>

              <button
                type="button"
                class="btn btn-sm btn-outline-danger mb-2"
                @click="remove(item)"
              >
                Remover
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="table-responsive d-none d-md-block">
        <table class="table table-striped table-bordered">
          <thead class="thead-dark">
            <tr>
              <th v-for="field in fields" :key="field.key">
                {{ field.label }}
              </th>
              <th>Ações</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in items" :key="item.id">
              <td v-for="field in fields" :key="field.key">
                {{ displayValue(field, item) }}
              </td>
              <td>
                <button
                  class="btn btn-sm btn-outline-info mr-1 mb-1"
                  @click="selected = item"
                >
                  Ver
                </button>
                <button
                  class="btn btn-sm btn-outline-primary mr-1 mb-1"
                  @click="edit(item)"
                >
                  Editar
                </button>
                <button
                  class="btn btn-sm btn-outline-danger mb-1"
                  @click="remove(item)"
                >
                  Remover
                </button>
              </td>
            </tr>
            <tr v-if="items.length === 0">
              <td :colspan="fields.length + 1" class="text-center">
                Não existem registos.
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <p class="text-muted">
        Protótipo académico. Dados locais de demonstração, sem ligação à API.
      </p>
    </b-container>
  </main>
</template>

<script>
import HeaderPage from "@/components/HeaderPage.vue";

export default {
  name: "EntityManager",
  components: { HeaderPage },
  props: {
    title: { type: String, required: true },
    singular: { type: String, required: true },
    description: { type: String, required: true },
    entityKey: { type: String, required: true },
    fields: { type: Array, required: true },
    initialItems: { type: Array, required: true }
  },
  data() {
    return {
      items: [],
      editing: false,
      editId: null,
      form: {},
      selected: null
    };
  },
  computed: {
    storageKey() {
      return "animalec-prototipo-" + this.entityKey;
    }
  },
  created() {
    try {
      const saved = localStorage.getItem(this.storageKey);
      const parsed = saved === null ? null : JSON.parse(saved);
      this.items = Array.isArray(parsed)
        ? parsed
        : this.initialItems.map(item => ({ ...item }));
    } catch (error) {
      this.items = this.initialItems.map(item => ({ ...item }));
    }
  },
  methods: {
    displayValue(field, item) {
      const value = item[field.key];

      if (value === undefined || value === null || value === "") {
        return "Não indicado";
      }

      if (field.options) {
        const option = field.options.find(entry => entry.value === value);

        if (option) {
          return option.label;
        }
      }

      return value;
    },
    isLegacyOption(field) {
      const value = this.form[field.key];
      return Boolean(
        value &&
          field.options &&
          !field.options.some(option => option.value === value)
      );
    },
    add() {
      this.editId = null;
      this.form = {};
      this.fields.forEach(field => {
        this.$set(this.form, field.key, "");
      });
      this.selected = null;
      this.editing = true;
    },
    edit(item) {
      this.editId = item.id;
      this.form = { ...item };
      this.selected = null;
      this.editing = true;
    },
    cancel() {
      this.editing = false;
      this.editId = null;
    },
    persist() {
      try {
        localStorage.setItem(this.storageKey, JSON.stringify(this.items));
      } catch (error) {
        window.alert("Não foi possível guardar os dados no browser.");
      }
    },
    save() {
      if (this.editId === null) {
        this.items.push({
          ...this.form,
          id:
            Date.now() +
            "-" +
            Math.random()
              .toString(36)
              .slice(2)
        });
      } else {
        const index = this.items.findIndex(item => item.id === this.editId);
        if (index < 0) return;
        this.$set(this.items, index, {
          ...this.form,
          id: this.editId
        });
      }
      this.persist();
      this.cancel();
    },
    remove(item) {
      if (!window.confirm("Remover este registo?")) return;
      this.items = this.items.filter(x => x.id !== item.id);
      this.selected = null;
      this.persist();
    }
  }
};
</script>
