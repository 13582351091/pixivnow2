<template lang="pug">
footer.global-footer
  .top.flex.container
    section.flex-1
      h4 探索更多
      ul
        li
          external-link(href="/api/illust/random?format=image") 随机图片
        li
          router-link(to="/ranking") 今日排行
        li
          router-link(to="/about") 关于本站
    section.flex-1
      h4 联系站长
      ul
        li
          | Telegram：
          external-link(:href="`https://t.me/Lcfstar`").
        li
          | Discord：
          external-link(:href="`https://discord.gg/zxAX5Jh`").
        li
          | Twitter：
          external-link(:href="`https://twitter.com/rogerxa77977892?t=KbR3EkHmiUxjxvHiFpsb7w&s=09`").
    //- section.flex-1
    //-   h4 社交媒体
    //-     p Placeholder
    section.flex-1
      h4 友情链接
      div 快来联系站长 交换友链吧~
      //- ul
      //-   li 链接

  .bottom.align-center
    p.copyright
      | &copy; Copyright {{ yearStr }}
      |
      a(:href="GITHUB_URL" target="_blank").
        {{ PROJECT_NAME }}
      |
      em v{{ version }}
    .dev-only(style="font-style: italic")
      | This is test site →&nbsp;
      a(
        :href="'https://pixiv.cocomi.eu.org' + $route.path"
        target="_blank"
      ) Go to Prod.
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { GITHUB_URL, PROJECT_NAME, GITHUB_OWNER } from '../config'
import { version } from '../../package.json'

const yearStr = ref(`2021 - ${new Date().getFullYear()}`)
</script>
<style scoped lang="sass">

.global-footer
  background-color: var(--theme-accent-color)
  font-size: 1rem
  color: var(--theme-accent-link-color)

.top
  padding-top: 2rem
  padding-bottom: 2rem
  gap: 1.5rem

.bottom
  padding-top: 0.5rem
  padding-bottom: 0.5rem

a
  --color: #eee
  font-weight: 600

  &::after
    visibility: visible
    transform: scaleX(1)
    width: 40%
    height: 1px

  &:hover::after
    width: 100%

.bottom
  background-color: var(--theme-accent-color-darken)

h4
  position: relative
  margin: 1rem 0 0.5rem 0
  padding-bottom: 0.2rem
  border-bottom: 2px solid
  font-size: 1.1rem

ul
  padding-left: 1rem
  margin: 0.2rem 0

  a
    display: inline
    font-weight: 400

@media screen and (max-width: 600px)
  .top
    flex-direction: column
</style>
