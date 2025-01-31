<template>
  <div>
    <pre>
      {{ data }}
    </pre>
  </div>
</template>

<script setup lang="ts">
const router = useRouter()

interface PublicPathwayCertificateDto {
  certificateId: string
  userName: String
  certificateImageMediaId: string
  certificatePdfMediaId: string
}

useSeoMeta({
  title: 'My Amazing Site',
  ogTitle: 'My Amazing Site',
  description: 'This is my amazing site, let me tell you all about it.',
  ogDescription: 'This is my amazing site, let me tell you all about it.',
  ogImage: 'https://example.com/image.png',
  twitterCard: 'summary_large_image',
})

const { data } = useAsyncData(
  `test`,
  async () => {
    // return a dictionary of cohorts
    const certificateid = '1'
    const contentHeaders = new Headers({
      'X-KINNU-CLIENT-VERSION': `1`,
    })

    try {
      const d = await $fetch<PublicPathwayCertificateDto>(`https://api.v2.kinnu.xyz/certification/pathway-certificate/public/${certificateid}`, {
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