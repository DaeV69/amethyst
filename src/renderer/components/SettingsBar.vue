<template>
  <padded-container>

    <settings-category-splitter text="UI" />
    <settings-binary-switch text="Color UI based on cover art" v-model="state.settings.colorInterfaceFromCoverart" />


    <settings-category-splitter text="Covers" />
    <settings-binary-switch text="Show cover art" v-model="state.settings.showCoverArt" />

    <settings-category-splitter text="Queue List" />
    <settings-binary-switch text="Show mini covers" v-model="state.settings.showMiniCovers" />

    <settings-category-splitter text="Spectrum" />
    <settings-binary-switch text="Enabled" v-model="state.settings.showSpectrum" />
    <settings-binary-switch text="Logarithmic Spectrum" v-model="state.settings.useLogarithmicSpectrum" />
    <settings-modifier text="Vertical zoom" :min="0.5" :max="2" :step="0.1" :default="1.5"
      v-model="state.settings.spectrumVerticalZoom" />
    <settings-modifier text="Smoothing" :min="0.01" :max="0.99" :step="0.01" :default="0.5"
      v-model="state.settings.spectrumSmoothing" />
    <settings-modifier text="FFT Size" :range="[32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768]"
      :default="8192" v-model="state.settings.spectrumFftSize" />

    <settings-category-splitter text="dB Meter" />
    <settings-binary-switch text="Enabled" v-model="state.settings.showDbMeter" />
    <settings-binary-switch text="Show instant dB values" v-model="state.settings.showInstantDecibelValues" />
    <settings-binary-switch text="Show average dB values" v-model="state.settings.showAverageDecibelValues" />

    <settings-category-splitter text="Audio Routing" />
    <settings-setting text="Output L/R">
      <select v-model="selectedOutputDevice" class="font-small text-7px w-full py-1 bg-surface-700">
        <option v-for="output of player.state.outputDevices">{{
        output.label
        }}</option>
      </select>
    </settings-setting>

    <settings-category-splitter text="Integrations" />
    <settings-binary-switch text="Discord Rich Presence" v-model="state.settings.discordRichPresence" />

    <div class="opacity-20 flex-col flex gap-2">
      <splitter />
      <div class="flex justify-between items-center">
        Made by: <img src="../geoxor_logo.svg" class="h-2" alt="">
      </div>
    </div>

  </padded-container>
</template>

<script setup lang="ts">
import { usePlayer, useState } from '../amethyst';
import SettingsCategorySplitter from './settings/SettingsCategorySplitter.vue';
import SettingsBinarySwitch from './settings/SettingsBinarySwitch.vue';
import SettingsModifier from './settings/SettingsModifier.vue';
import PaddedContainer from './PaddedContainer.vue';
import { ref, watch } from 'vue';
import SettingsSetting from './settings/SettingsSetting.vue';
import Splitter from './Splitter.vue';
const state = useState();
const player = usePlayer();

const selectedOutputDevice = ref(player.state.outputDevices.find(device => device.deviceId === player.state.selectedOutputDeviceId)?.label || "Unset");
watch(() => selectedOutputDevice.value, () => player.updateOutputDevice(player.state.outputDevices.find(device => device.label === selectedOutputDevice.value)?.deviceId!));


</script>
