<script>
    import { browser } from "$app/environment";
    import { draggable } from "@neodrag/svelte";
    let position = (browser &&
        JSON.parse(localStorage.getItem("position"))) || { x: 0, y: 0 };
    let isDisabled = true;
</script>

<div
    class="text-center"
    on:click={() => (isDisabled = !isDisabled)}
    id="a"
    use:draggable={{
        position,
        disabled: isDisabled,
        onDrag: ({ offsetX, offsetY }) => {
            position = { x: offsetX, y: offsetY, id: "a" };
            localStorage.setItem("position", JSON.stringify(position));
        },
    }}
>
    <h1 class="text-4xl font-extrabold text-blue">可能にする</h1>
    <p>Cepi Herdiansyah</p>
</div>
