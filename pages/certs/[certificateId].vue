<template>
  <div>
    <pre>
      {{ certId }}
    </pre>
    <h1 class="text-3xl font-bold underline"> Hello world! </h1>
  </div>
</template>

<script setup lang="ts">
const route = useRoute()

const certId = route.params.certificateId

const { data } = useAsyncData(
  `test`,
  async () => {
    // return a dictionary of cohorts
    const certificateid = '1'
    const contentHeaders = new Headers({
      'X-KINNU-CLIENT-VERSION': `1`,
    })

    try {
      const d = await $fetch(`https://api.v2.kinnu.xyz/certification/pathway-certificate/public/${certificateid}`, {
        headers: contentHeaders,
      })
      console.log(d)
      return d
    }
    catch (e) {
      console.error(e)
      return []
    }
  },
)
</script>

<style scoped></style>