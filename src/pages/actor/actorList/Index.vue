<template>
  <q-page class="q-page q-pa-lg">
    <div class="row justify-center">
      <div class="col-9 q-px-xl q-pb-xl bg-brand">
        <h4>演員</h4>
        <div class="row items-start q-col-gutter-md">
          <div
            v-for="actor in actors"
            :key="actor.id"
            class="col-lg-3 col-md-4 col-sm-6 col-xs-12"
          >
            <router-link :to="`/actor/${actor.id}`">
              <q-card>
                <img :src="actor.avatar" />
                <q-card-section>
                  <div class="text-center">{{ actor.translatedName }}</div>
                </q-card-section>
              </q-card>
            </router-link>
          </div>
        </div>
        <div class="q-pa-lg flex flex-center">
          <q-pagination
            v-model="currentPage"
            :max="lastPage"
            direction-links
          ></q-pagination>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { api } from "boot/axios";
import { Notify } from "quasar";
import { watch } from "vue";

export default defineComponent({
  name: "ActorPage",
  setup() {
    const currentPage = ref(1);
    const lastPage = ref(1);

    const actors = ref([]);
    const getActors = async () => {
      try {
        const response = await api.get(
          `/actor?current_page=${currentPage.value}`
        );
        actors.value = response.data.data;
        lastPage.value = response.data.pagination.lastPage;
      } catch (error) {
        console.log(error);
        Notify.create(error);
      }
    };
    getActors();

    // 翻頁時重新取得資料
    watch(currentPage, (newValue, oldValue) => {
      if (newValue != oldValue) {
        getActors();
      }
    });

    return {
      currentPage,
      lastPage,
      actors,
    };
  },
});
</script>
