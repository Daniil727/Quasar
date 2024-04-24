<template>
  <div>
    <div class="q-pa-md">
      <q-carousel animated v-model="slide" arrows navigation infinite>
        <q-carousel-slide :name="1" img-src="https://loremflickr.com/640/360/1" />
        <q-carousel-slide :name="2" img-src="https://loremflickr.com/640/360/2" />
        <q-carousel-slide :name="3" img-src="https://loremflickr.com/640/360/3" />
        <q-carousel-slide :name="4" img-src="https://loremflickr.com/640/360/4" />
      </q-carousel>
    </div>

    <div>
      <q-splitter class="splitterStyle" v-model="splitterModel">

        <template v-slot:before>
          <div class="q-pa-md">
            <div class="text-h4 q-mb-md">Before</div>
            <div v-for="n in 20" :key="n" class="q-my-md">{{ n }}. Lorem ipsum dolor sit, amet consectetur adipisicing
              elit. Quis praesentium cumque magnam odio iure quidem, quod illum numquam possimus obcaecati commodi
              minima
              assumenda consectetur culpa fuga nulla ullam. In, libero.</div>
          </div>
        </template>

        <template v-slot:after>
          <div class="q-pa-md">
            <div class="text-h4 q-mb-md">After</div>
            <div v-for="n in 20" :key="n" class="q-my-md">{{ n }}. Lorem ipsum dolor sit, amet consectetur adipisicing
              elit. Quis praesentium cumque magnam odio iure quidem, quod illum numquam possimus obcaecati commodi
              minima
              assumenda consectetur culpa fuga nulla ullam. In, libero.</div>
          </div>
        </template>

      </q-splitter>
    </div>



    <div class="q-pa-md formStyle">

      <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
        <q-input filled v-model="name" label="Your name *" hint="Name and surname" lazy-rules
          :rules="[val => val && val.length > 0 || 'Please type something']" />

        <q-input filled type="number" v-model="age" label="Your age *" lazy-rules :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]" />

        <q-toggle v-model="accept" label="I accept the license and terms" />

        <div>
          <q-btn label="Submit" type="submit" color="primary" />
          <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script setup>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

const slide = ref(1);
const splitterModel = ref(50);

defineOptions({
  name: 'IndexPage'
});

//form

const $q = useQuasar();
const name = ref(null);
const age = ref(null);
const accept = ref(false);

function onSubmit() {
  if (accept.value !== true) {
    $q.notify({
      color: 'red-5',
      textColor: 'white',
      icon: 'warning',
      message: 'You need to accept the license and terms first'
    })
  }
  else {
    $q.notify({
      color: 'green-4',
      textColor: 'white',
      icon: 'cloud_done',
      message: 'Submitted'
    })
  }
};
function onReset() {
  name.value = null
  age.value = null
  accept.value = false
};

</script>

<style>
.formStyle {
  margin: 0 auto;
  max-width: 400px;
}

.splitterStyle {
  height: 400px;
}
</style>