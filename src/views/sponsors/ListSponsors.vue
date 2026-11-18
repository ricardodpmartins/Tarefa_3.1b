<template>
  <EntityManager
    title="Gestão de Sponsors"
    singular="patrocinador"
    description="Gestão dos patrocinadores associados aos animais."
    entity-key="sponsors"
    :fields="fields"
    :initial-items="initialItems"
  />
</template>

<script>
import EntityManager from "@/components/admin/EntityManager.vue";

export default {
  name: "ListSponsors",
  components: { EntityManager },
  data() {
    return {
      fields: [
        { key: "nome", label: "Nome" },
        { key: "tipo", label: "Tipo" },
        {
          key: "animal",
          label: "Animal associado",
          options: [
            { value: "Cão", label: "Cão" },
            { value: "Gato", label: "Gato" },
            { value: "Pardal", label: "Pardal" },
            { value: "Cavalo", label: "Cavalo" }
          ]
        },
        { key: "email", label: "Email", type: "email" }
      ],
      initialItems: [
        {
          id: "s1",
          nome: "Patrocinador Exemplo",
          tipo: "Empresa",
          animal: "Cão",
          email: "exemplo@invalid.example"
        }
      ]
    };
  }
};
</script>
