<template>
    <div class="flex justify-center bg-gradient-to-b from-gray-900 to-purple-900 items-center min-h-screen p-4">
        <div v-if="finished" class="text-center p-4 md:p-8 bg-black/30 rounded-xl backdrop-blur-sm border border-purple-500/30 shadow-2xl max-w-full sm:max-w-lg md:max-w-xl">
            <h1 class="text-3xl sm:text-4xl md:text-5xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-purple-400 to-pink-500 animate-pulse">
                Happy 18th Birthday, Exotical! 🎉
            </h1>
            <div class="mt-4 md:mt-8">
                <div class="py-4 md:py-6 px-4 md:px-8 animate-bounce bg-gradient-to-r from-purple-500 to-pink-500 rounded-full text-white text-xl md:text-2xl font-bold">
                    It's finally here!
                </div>
                <div class="mt-4 md:mt-6 grid grid-cols-3 gap-2 md:gap-4">
                    <span class="text-4xl md:text-6xl">🎂</span>
                    <span class="text-4xl md:text-6xl">🎈</span>
                    <span class="text-4xl md:text-6xl">🎁</span>
                </div>
            </div>
        </div>
        <div v-else class="text-center p-4 md:p-8 bg-black/30 rounded-xl backdrop-blur-sm border border-purple-500/30 shadow-2xl w-full max-w-xs sm:max-w-lg md:max-w-xl">
            <h1 class="text-4xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-purple-400 to-pink-500">
                Exotical's 18th Birthday
            </h1>
            <p class="text-sm md:text-base">April 30, 2025 (2025-04-30)</p>
            <p class="text-lg md:text-2xl mt-2 md:mt-4 text-cyan-300">Time remaining (CEST):</p>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 md:gap-4 mt-4 md:mt-8">
                <div class="flex flex-col p-2 md:p-4 bg-black/50 rounded-lg border border-purple-500/50">
                    <span class="text-4xl md:text-6xl font-bold text-white">{{ days }}</span>
                    <span class="text-sm md:text-lg text-gray-300">days</span>
                </div>
                <div class="flex flex-col p-2 md:p-4 bg-black/50 rounded-lg border border-purple-500/50">
                    <span class="text-4xl md:text-6xl font-bold text-white">{{ hours }}</span>
                    <span class="text-sm md:text-lg text-gray-300">hours</span>
                </div>
                <div class="flex flex-col p-2 md:p-4 bg-black/50 rounded-lg border border-purple-500/50">
                    <span class="text-4xl md:text-6xl font-bold text-white">{{ minutes }}</span>
                    <span class="text-sm md:text-lg text-gray-300">minutes</span>
                </div>
                <div class="flex flex-col p-2 md:p-4 bg-black/50 rounded-lg border border-purple-500/50">
                    <span class="text-4xl md:text-6xl font-bold text-white">{{ seconds }}</span>
                    <span class="text-sm md:text-lg text-gray-300">seconds</span>
                </div>
            </div>
            <div class="flex justify-center items-center gap-2 mt-6">
                <UIcon name="i-fa6-brands-github" />
                <ULink to="https://github.com/ItzExotical/BirthdayCountdown">
                    Source code
                </ULink>
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
    import { DateTime } from "luxon";
    const birthday = DateTime.fromISO("2025-04-30T00:00:00", {zone: "Europe/Stockholm"});
    const finished = ref(Boolean());
    const days = ref(Number());
    const hours = ref(Number());
    const minutes = ref(Number());
    const seconds = ref(Number());
    const updateCountdown = () => {
        const now = DateTime.now().setZone("Europe/Stockholm");
        const diff = birthday.diff(now, ["days", "hours", "minutes", "seconds"]);
        if (diff.toMillis() <= Number()) {
            days.value = Number();
            hours.value = Number();
            minutes.value = Number();
            seconds.value = Number();
            finished.value = Boolean(1);
            if (intervalId !== null) clearInterval(intervalId);
        } else {
            days.value = Math.floor(diff.days);
            hours.value = Math.floor(diff.hours);
            minutes.value = Math.floor(diff.minutes);
            seconds.value = Math.floor(diff.seconds);
        };
    };
    let intervalId: ReturnType<typeof setInterval> | null = null;
    onMounted(() => {
        updateCountdown();
        intervalId = setInterval(updateCountdown, 1000);
    });
    onUnmounted(() => {
        if (intervalId !== null) clearInterval(intervalId);
    });
</script>