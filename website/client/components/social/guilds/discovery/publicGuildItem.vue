<template lang="pug">
.card
  .card-block
    .clearfix
      router-link.float-left(:to="{ name: 'guild', params: { guildId: guild._id } }")
        h3 {{ guild.name }}
      button.btn.float-right(:class="[isMember ? 'btn-danger' : 'btn-success']") {{ isMember ? $t('leave') : $t('join') }}
    p {{ guild.description }}
</template>

<style lang="scss" scoped>
.card {
  margin-bottom: 1rem;
}
</style>

<script>
import { mapState } from 'client/libs/store';
import groupUtilities from 'client/mixins/groupsUtilities';

export default {
  mixins: [groupUtilities],
  props: ['guild'],
  computed: {
    ...mapState({user: 'user.data'}),
    isMember () {
      return this.isMemberOfGroup(this.user, this.guild);
    },
  },
};
</script>