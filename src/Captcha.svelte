<script>
    import { fade } from "svelte/transition";

    export let title = "Prove that you are not a robot",
        buttonLabel = "Change Captcha",
        style = "background-color:#333;",
        width = 160,
        height = 60,
	fontSize = 40,
        answer = "";

    let captcha = "";
    let verified = false;

    import { createEventDispatcher, onMount } from "svelte";
    const dispatch = createEventDispatcher();
    dispatch("ok", true);

    Array.prototype.sample = function () {
        return this[Math.floor(Math.random() * (this.length - 1))];
    };

    function genCaptcha() {
        var first = "1,3,6,86,7,8,9,9,8,55,65,4,5,7,8,97,6,4,4,6,7,4,16"
            .split(",")
            .sample();
        var second = "6,7,6,4,14,15,18,9,8,6,54,3,2,2,4,67,6,9,8,5,3,35"
            .split(",")
            .sample();
        var operator = ["*", "/", "+", "-"].sample();

        captcha = first + " " + operator + " " + second;
        var canvas = document.getElementById("canvas");
        var ctx = canvas.getContext("2d");
        ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);
        ctx.beginPath();
        ctx.font = fontSize + "px Cursive";
	ctx.textAlign = "center";
        ctx.fillStyle = "#E6C200";
        ctx.fillText(captcha, width/2, height*0.75);
    }

    onMount(() => {
        setTimeout(() => genCaptcha(), 2000);
    });

    $: {
        const evaluate = new Function('return '+ captcha);
        if (evaluate() === answer * 1) verified = true;
        else verified = false;
    }
    $: dispatch("verified", verified);
</script>

<div transition:fade>
    <h4>
        <slot name="title">{title}<br /><br /></slot>
        <canvas id="canvas" {style} width="{width}px" height="{height}px">
	  Your browser does not support the HTML5 canvas tag.
	</canvas><br />
        <button type="button" class="danger" on:click|preventDefault={genCaptcha}><slot
                name="button-label">
                {buttonLabel}
            </slot></button>
    </h4>
</div>
