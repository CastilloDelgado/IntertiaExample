<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Módulo de Notas
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="md:grid md:grid-cols-3 md:gap-6">
          <div class="md:col-span-1">
            <div class="p3-4 sm:px0">
              <h3 class="text-lg text-gray-900">Editar una nota</h3>
              <p class="text-sm text-gray-600">
                Si editas, no podrás volver al estado anterior de la nota.
              </p>
            </div>
          </div>
          <div class="md:col-span-2 mt-5 md:mt-0">
            <div class="shadow bg-white md:rounded-md p-4">
              <form @submit.prevent="submit">
                <label class="block font-medium text-sm text-gray-700"
                  >Resumen</label
                >
                <textarea
                  class="form-input w-full rounded-md shadow-sm"
                  v-model="form.excerpt"
                ></textarea>
                <label class="block font-medium text-sm text-gray-700"
                  >Contenido</label
                >
                <textarea
                  rows="10"
                  class="form-input w-full rounded-md shadow-sm"
                  v-model="form.content"
                ></textarea>
                <button
                  class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md"
                >
                  Editar
                </button>
                <hr class="my-2" />
                <a
                  class="bg-red-500 px-2 py-2 text-white hover:bg-red-700 rounded-md font-bold"
                  href="#"
                  @click.prevent="destroy"
                >
                  Eliminar Nota
                </a>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";

export default {
  components: {
    AppLayout,
  },
  props: {
    note: Object,
  },
  data() {
    return {
      form: {
        excerpt: this.note.excerpt,
        content: this.note.content,
      },
    };
  },

  methods: {
    submit() {
      this.$inertia.put(this.route("notes.update", this.note.id), this.form);
    },
    destroy() {
      if (confirm("¿Desea eliminar esta nota?")) {
        this.$inertia.delete(this.route("notes.destroy", this.note.id));
      }
    },
  },
};
</script>
