<script lang="ts">
import { DARK_MODE, LIGHT_MODE } from "@constants/constants.ts";
import Icon from "@iconify/svelte";
import {
	applyThemeToDocument,
	getStoredTheme,
	setTheme,
} from "@utils/setting-utils.ts";
import { onMount } from "svelte";
import type { LIGHT_DARK_MODE } from "@/types/config.ts";

let mode: LIGHT_DARK_MODE = $state(LIGHT_MODE);

onMount(() => {
	mode = getStoredTheme();
	applyThemeToDocument(mode);
});

function toggleScheme() {
	mode = mode === LIGHT_MODE ? DARK_MODE : LIGHT_MODE;
	setTheme(mode);
}
</script>

<div class="relative z-50">
	<button
		aria-label="Light/Dark Mode"
		class="relative btn-plain scale-animation rounded-lg h-11 w-11 active:scale-90"
		id="scheme-switch"
		onclick={toggleScheme}
	>
		<div class="absolute" class:opacity-0={mode !== LIGHT_MODE}>
			<Icon
				icon="material-symbols:wb-sunny-outline-rounded"
				class="text-[1.25rem]"
			/>
		</div>
		<div class="absolute" class:opacity-0={mode !== DARK_MODE}>
			<Icon
				icon="material-symbols:dark-mode-outline-rounded"
				class="text-[1.25rem]"
			/>
		</div>
	</button>
</div>
