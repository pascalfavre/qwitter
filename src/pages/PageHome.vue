<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
        <q-input
          class="new-qweet"
          bottom-slots
          v-model="newQweetContent"
          placeholder="What's happening ?"
          counter
          maxlength="280"
          autogrow
        >
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://cdn.quasar.dev/img/avatar1.jpg" />
            </q-avatar>
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn
          class="q-mb-lg"
          unelevated
          rounded
          color="primary"
          label="Qweet"
          no-caps
          :disable="!newQweetContent"
        />
      </div>
    </div>
    <q-separator size="10px" color="grey-2" class="divider" />

    <q-list separator>
      <q-item 
        class="q-py-md"
        v-for="qweet in qweets"
        :key="qweet.date"
      >
        <q-item-section top avatar>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar1.jpg" />
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1">
            <strong>Pascal favre</strong>
            <span class="text-grey-7">@pascal.favre</span>
          </q-item-label>
          <q-item-label class="text-body1 qweet-content">
            {{ qweet.content }}
          </q-item-label>
          <div class="qweet-icons row justify-between q-mt-sm">
            <q-btn flat round color="grey" size="sm" icon="far fa-comment" />
            <q-btn flat round color="grey" size="sm" icon="fas fa-retweet" />
            <q-btn flat round color="grey" size="sm" icon="far fa-heart" />
            <q-btn flat round color="grey" size="sm" icon="fas fa-trash" />
          </div>
        </q-item-section>

        <q-item-section side top> {{ relativeDate(qweet.date) }} </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { formatDistance } from 'date-fns'

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newQweetContent: null,
      qweets: [
        {
          content: "Lorem ipsum dolor, sit amet consectetur adipisicing elit. Vero, doloribus voluptas! Nostrum placeat modi deleniti optio magnam perferendis atque laudantium mollitia. Ea, optio natus vero sint consectetur deleniti repudiandae dolore.",
          date: 1643633332307
        },
        
        {
          content: "Lorem ipsum dolor, sit amet consectetur adipisicing elit. Vero, doloribus voluptas! Nostrum placeat modi deleniti optio magnam perferendis atque laudantium mollitia. Ea, optio natus vero sint consectetur deleniti repudiandae dolore.",
          date: 1643633348125
        }
      ]
    };
  },
  methods: {
    relativeDate(value) {
      return formatDistance(value, new Date());
    }
  }
});
</script>

<style lang="sass">
.new-qweet
  textarea
    font-size:19px
    line-height:1.4 !important

.divider
  border-top:1px solid
  border-bottom:1px solid
  border-color: $grey-4

.qweet-content
  white-space:pre-line

.qweet-icons
  margin-left:-5px
</style>
