<template>
    <div class="oops">
        {{text}}</div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

@Component
export default class DynamicWord extends Vue {
    @Prop({
        required: true,
        type: String
    }) private text!: string;

    public mounted() {
        this.dealText();
    }

    /**
     * dealText
     */
    public dealText() {
        const oops: any = document.querySelector(".oops");
        const letters: Array < string > = oops.textContent.split("");
        oops.textContent = "";
        letters.forEach((letter, i) => {
            const span = document.createElement("span");
            span.textContent = letter;
            span.style.animationDelay = `${i / 10}s`;
            oops.append(span);
        });
    }
}
</script>

<style scoped lang="scss">
@function float-text-3d($shadow-color: #e86131, $depth: 10, $floating: false) {
    $shadows: ();
    @for $i from 1 to $depth {
        @if ($floating==false and $i > $depth / 2) {
            $shadow-color: transparent;
        }
        $shadows: append($shadows, 0 ($i * 1px) $shadow-color, comma);
    }
    @if ($floating==false) {
        $shadows: append($shadows, 0 10px 10px rgba(0, 0, 0, 0.4), comma);
    }
    @else {
        $shadows: append($shadows, 0 50px 25px rgba(0, 0, 0, 0.2), comma);
    }
    @return $shadows;
}

.oops {
    display: flex;
    color: white;
    font-size: 100px;
    font-family: "Baloo Bhaijaan";
    text-transform: uppercase;
    ::v-deep {
        span {
            text-shadow: float-text-3d($floating: false);
            transform: translateY(20px);
            animation: bounce 0.3s ease infinite alternate;
        }
    }
}

@keyframes bounce {
    to {
        text-shadow: float-text-3d($floating: true);
        transform: translateY(-20px);
    }
}
</style>