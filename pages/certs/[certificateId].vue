<template>
  <div>
  </div>
</template>

<script setup lang="ts">
const route = useRoute()

interface PublicPathwayCertificateDto {
  certificateId: string
  userName: String
  certificateImageMediaId: string
  certificatePdfMediaId: string
}

const data = ref<PublicPathwayCertificateDto | null>(null)

onBeforeMount(async () => {
  // return a dictionary of cohorts
  const certificateid = route.params.certificateId
  const contentHeaders = new Headers({
    'X-KINNU-CLIENT-VERSION': `1`,
  })

  try {
    const d = await $fetch<PublicPathwayCertificateDto>(`https://api.v2.kinnu.xyz/certification/pathway-certificate/public/${certificateid}`, {
      headers: contentHeaders,
    })
    // console.log(d)
    // const d = {
    //   certificateId: '1',
    //   userName: 'John Doe',
    //   certificateImageMediaId: '1',
    //   certificatePdfMediaId: '1',
    // }

    useSeoMeta({
      title: `${d.userName}'s Certificate`,
      ogTitle: `${d.userName}'s Certificate`,
      description: 'This is my amazing site, let me tell you all about it.',
      ogDescription: 'This is my amazing site, let me tell you all about it.',
      ogImage: `https://api.v2.kinnu.xyz/media/${d.certificateImageMediaId}/MEDIUM`,
      twitterCard: 'summary_large_image',
    })
  }
  catch (e) {
    console.error(e)
    return []
  }
})
</script>

<style scoped></style>