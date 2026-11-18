<template>
  <EntityManager
    title="Gestão de Experts"
    singular="especialista"
    description="Gestão dos especialistas científicos."
    entity-key="experts"
    :fields="fields"
    :initial-items="initialItems"
  />
</template>

<script>
import EntityManager from "@/components/admin/EntityManager.vue";

export default {
  name: "ListExperts",
  components: { EntityManager },
  data() {
    return {
      fields: [
        { key: "nome", label: "Nome" },
        { key: "especialidade", label: "Especialidade" },
        {
          key: "grupo",
          label: "Grupo animal",
          options: [
            { value: "anfibio", label: "Anfíbio" },
            { value: "ave", label: "Ave" },
            { value: "mamifero", label: "Mamífero" },
            { value: "peixe", label: "Peixe" },
            { value: "reptil", label: "Réptil" }
          ]
        },
        { key: "email", label: "Email", type: "email" }
      ],
      initialItems: [
        {
          id: "e1",
          nome: "Especialista Exemplo",
          especialidade: "Zoologia",
          grupo: "Mamíferos",
          email: "exemplo@invalid.example"
        }
      ]
    };
  }
};
</script>
