<template>
  <div class="wrapper">
    <DamagePane class="wrapper-pane" :record="demoRecord" />
  </div>
</template>
<script setup lang="ts">
  import type { PlayerState, RecordState } from '@/store/record';
  import DamagePane from '../damage/DamagePane.vue';
  import { actors } from '@/utils/enums';

  const players: PlayerState[] = [];

  let totalDamage = 9_876_543_210;
  let damageInSecond = 98_765;
  let damageInMinute = 9_876_543;
  let damageInMinutePerSecond = 98_765;
  for (let i = 0; i < 4; ++i) {
    players.push({
      id: Number.parseInt(actors[i], 16),
      index: i,
      totalDamage: [totalDamage],
      damageInSecond: [damageInSecond],
      damageInMinute: [damageInMinute],
      damageInMinutePerSecond: [damageInMinutePerSecond],
      targets: [],
      actions: [],
    });

    totalDamage = Math.floor(totalDamage / 10);
    damageInSecond = Math.floor(damageInSecond / 10);
    damageInMinute = Math.floor(damageInMinute / 10);
    damageInMinutePerSecond = Math.floor(damageInMinutePerSecond / 10);
  }

  const demoRecord: RecordState = {
    id: 'demo',
    startTimestamp: Date.now() - 1000,
    lastTimestamp: Date.now(),
    players,
    messages: [],
  };
</script>

<style scoped lang="less">
  .wrapper {
    padding: 16px;

    width: 100%;
    height: 250px;

    // Background
    background-image: linear-gradient(45deg, #ccc 25%, transparent 25%),
      linear-gradient(135deg, #ccc 25%, transparent 25%), linear-gradient(45deg, transparent 75%, #ccc 75%),
      linear-gradient(135deg, transparent 75%, #ccc 75%);
    background-size: 24px 24px; /* Must be a square */
    background-position: 0 0, 12px 0, 12px -12px, 0px 12px; /* Must be half of one side of the square */

    // Border
    border: 1px solid #ccc;
    border-radius: 4px;
  }
</style>
