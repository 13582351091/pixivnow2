<template lang="pug">
.artwork-large-card
  .top
    router-link(:to="'/artworks/' + illust.id")
      .thumb
        img(
          v-if="!xRestrict"
          :src="resolveSrc(illust.url.replace('p0_master', 'p0_square'))"
          :alt="illust.title"
          lazyload)
      .x-restrict.tag(v-if="xRestrict" title="R-18")
        fa(icon="eye")
      .page-count(
        v-if="+illust.pageCount > 1"
        :title="'共 ' + illust.pageCount + ' 张'")
        fa(icon="images")
        | {{ illust.pageCount }}
      .ranking(
        v-if="rank !== 0"
        :class="{ gold: rank === 1, silver: rank === 2, bronze: rank === 3 }"
        :style="`font-size: ${rank > 99 ? 1 : 1.3}rem;`"
        ) {{ rank }}
  .bottom
    h3.title(:title="illust.title")
      router-link(:to="'/artworks/' + illust.id") {{ illust.title }}
    .author(:title="illust.userName")
      router-link(:to="'/users/' + illust.userId")
        img.avatar(
          :src="resolveSrc(illust.profileImageUrl)"
          lazyload
          )
        | {{ illust.userName }}
    .tags
      router-link.tag(v-for="tagName in illust.tags", :to="'/search/' + tagName") \#{{ tagName }}
</template>

<script lang="ts" setup>
import { computed } from 'vue';
import { useRoute } from 'vue-router';
import { API_BASE, resolveSrc } from '../../config'
import type { ArtworkInfo } from '../../types'

const props = defineProps<{
  illust: ArtworkInfo
  rank: number
}>()

const route = useRoute()
const xRestrict = computed(() => {
  if (route.name == 'ranking') return props.illust.xRestrict > 1
  return props.illust.xRestrict > 0
})
</script>

<style lang="sass">

h3
  margin-bottom: .4rem

.artwork-large-card
  display: inline-block
  box-sizing: border-box
  box-shadow: 0 0 4px #ccc
  padding: .4rem
  width: 24%
  min-width: 240px
  max-width: calc(50vw - 2rem)
  margin-bottom: 5px
  background-color: var(--theme-background-color)
  border-radius: 4px
  transition: all .24s ease-in-out

  &:hover
    box-shadow: var(--theme-box-shadow-hover)

@media screen and (max-width: 1150px)
  .artwork-large-card
    width: 32%
@media screen and (max-width: 865px)
  .artwork-large-card
    width: 48%
@media screen and (max-width: 578px)
  .artwork-large-card
    min-width: 100%

.top
  position: relative

  a
    display: block

  .thumb
    position: relative
    width: 100%
    height: 0
    padding-top: 100%
    animation: imgProgress 0.6s ease infinite alternate

    img
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      object-fit: cover

  .page-count
    position: absolute
    top: .4rem
    right: .4rem
    color: #fff
    background-color: rgba(0, 0, 0, 0.6)
    padding: .2rem .6rem
    border-radius: 1rem

    [data-icon]
      margin-right: .2rem

  .x-restrict
    position: absolute
    top: .2rem
    left: .2rem
    color: #fff
    background-color: rgb(255, 0, 0, 0.8)
    width: 2rem
    height: 2rem
    border-radius: 50%
    display: flex
    align-items: center

    [data-icon]
      margin: 0 auto

  .ranking
    position: absolute
    top: -1rem
    left: -1rem
    display: flex
    justify-content: center
    align-items: center
    width: 2rem
    height: 2rem
    font-size: 1.4rem
    font-weight: 600
    color: #252525
    background-color: #fff
    border-radius: 50%
    box-shadow: 0 0 0 2px rgba(var(--theme-accent-color--rgb), 0.4) inset, 0 0 0 4px #fff

    &.gold
      box-shadow: 0 0 0 2px gold inset, 0 0 0 4px #fff
    &.silver
      box-shadow: 0 0 0 2px darkgray inset, 0 0 0 4px #fff
    &.bronze
      box-shadow: 0 0 0 2px #b87333 inset, 0 0 0 4px #fff

.bottom

  .title a
    display: inline
  .author a
    display: inline-flex

  .title,
  .author
    white-space: nowrap
    text-overflow: ellipsis
    overflow: hidden
    width: 100%
    padding-bottom: 2px

    a
      align-items: center

      &.router-link-active
        color: var(--theme-text-color)
        font-weight: 600
        font-style: normal
        cursor: default

        &::after
          visibility: hidden

      .avatar
        display: inline-block
        width: 2rem
        height: 2rem
        box-sizing: border-box
        border: 2px solid #fff
        border-radius: 50%
        box-shadow: 0 0 4px #ccc
        margin-right: .4rem

  .author
    margin: .4rem 0

  .tags
    overflow: auto
    max-height: 140px

    .tag
      display: inline-block
      margin: 2px
      padding: 2px 4px
      background-color: #d6e4ff
      border-radius: 4px
</style>
