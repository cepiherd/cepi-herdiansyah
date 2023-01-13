<script>
    import { browser } from "$app/environment";
    import { draggable } from "@neodrag/svelte";
    let position = (browser &&
        JSON.parse(localStorage.getItem("position"))) || { x: 0, y: 0 };
    let isDisabled = true;
    let countdown = "";
    function countDownRamadhan() {
        var countDownDate = new Date("March 22, 2023 17:00:00").getTime();

        // Update the count down every 1 second
        var x = setInterval(function () {
            // Get today's date and time
            var now = new Date().getTime();

            // Find the distance between now and the count down date
            var distance = countDownDate - now;

            // Time calculations for days, hours, minutes and seconds
            var days = Math.floor(distance / (1000 * 60 * 60 * 24));
            var hours = Math.floor(
                (distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
            );
            var minutes = Math.floor(
                (distance % (1000 * 60 * 60)) / (1000 * 60)
            );
            var seconds = Math.floor((distance % (1000 * 60)) / 1000);

            // Display the result in the element with id="demo"
            countdown =
                days + "D " + hours + "H " + minutes + "M " + seconds + "S ";

            // If the count down is finished, write some text
            if (distance < 0) {
                clearInterval(x);
                countdown = "EXPIRED";
            }
        }, 1000);
    }

    $: countDownRamadhan();
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
    <div class="">
        <h1 class="text-4xl font-extrabold text-blue">ラマダン</h1>
        <p class="text-2xl text-center">{countdown}</p>
    </div>
    <h1 class="text-4xl font-extrabold text-blue">可能にする</h1>
    <p>Cepi Herdiansyah</p>
</div>
