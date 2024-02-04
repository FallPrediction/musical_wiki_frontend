<template>
  <q-page class="q-page q-pa-lg">
    <div class="row justify-center">
      <div class="col-9 q-px-xl q-pb-xl bg-dark">
        <h4>{{ actor.translatedName }}</h4>
        <div class="row reverse items-start">
          <q-card class="col-sm-4 char-card q-my-md">
            <img :src="actor.avatar" />
            <q-list>
              <q-item>
                <q-item-section avatar> 本名 </q-item-section>
                <q-item-section>
                  <q-item-label
                    >{{ actor.name }}({{ actor.translatedName }})</q-item-label
                  >
                </q-item-section>
              </q-item>

              <q-item>
                <q-item-section avatar> 暱稱 </q-item-section>
                <q-item-section>
                  <q-item-label>{{ actor.nickName }}</q-item-label>
                </q-item-section>
              </q-item>

              <q-item>
                <q-item-section avatar> 國籍 </q-item-section>
                <q-item-section>
                  <q-item-label>{{ actor.nationality }}</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>
          </q-card>
          <div class="col-sm-8 text-body1 q-pa-md" v-html="actor.content"></div>
          <div class="col-12 text-body1 q-pa-md">
            <h5 class="no-margin">出演作品</h5>
            <q-separator inset></q-separator>
            <q-list dense padding class="rounded-borders">
              <q-item v-for="credit in actor.credits" :key="credit.id">
                <q-item-section>
                  {{ credit.time }} {{ credit.place }}：{{ credit.musical }}
                  {{ credit.character }}
                </q-item-section>
              </q-item>
            </q-list>
          </div>
          <div class="col-12 q-pa-md">
            <h5 class="no-margin">圖片</h5>
            <q-separator inset></q-separator>
            <q-carousel
              animated
              v-model="nowGalleryId"
              arrows
              navigation
              infinite
            >
              <q-carousel-slide
                v-for="gallery in actor['gallery']"
                :name="gallery.id"
                :img-src="gallery.url"
                :key="gallery.id"
              ></q-carousel-slide>
              <template v-slot:control>
                <q-carousel-control position="bottom-right" :offset="[18, 18]">
                  <q-btn
                    push
                    round
                    dense
                    color="white"
                    text-color="primary"
                    :icon="'open_in_new'"
                    @click="openImg()"
                  ></q-btn>
                </q-carousel-control>
              </template>
            </q-carousel>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { api } from "boot/axios";
import { useRoute } from "vue-router";
import { Notify } from "quasar";

export default defineComponent({
  name: "ActorPage",
  setup() {
    const route = useRoute();

    const actor = ref({});
    const nowGalleryId = ref(1);
    const getActor = async () => {
      try {
        const response = await api.get(`/actor/${route.params.id}`);
        actor.value = response.data.data;
      } catch (error) {
        Notify.create(error.response.message);
      }
      nowGalleryId.value = actor.value.gallery[0].id;
    };
    getActor();

    const openImg = () => {
      const slide = actor.value["gallery"].find(
        (element) => element.id == nowGalleryId.value
      );
      window.open(slide.link, "_blank").focus();
    };

    return {
      nowGalleryId,
      openImg,
      actor,
    };
  },
});
</script>
