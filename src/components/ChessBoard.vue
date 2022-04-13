<!-- ChessBoard Component -->
<script setup>
import { reactive } from 'vue';
import Card from './Card.vue';

const props = defineProps({
    cards: Array,
    backCardImage: String
});

// Vamos a definir un evento que se va a disparar cuando dos parejas seleccionadas sean correctas
const emit = defineEmits(['onCheckedCards'])

const cardsDoubled =[...props.cards,...props.cards];
shuffleArray(cardsDoubled);

// Variable de estado que guarde las cartas seleccionadas hasta el momento
let selectedCards = [];

const cardsChessBoard = reactive(cardsDoubled.map((card) => {
    return {
        ...card,
        reveal: false
    }
}));

function shuffleArray(inputArray) {
    inputArray.sort(() => Math.random() - 0.5);
}

function onCardClicked(card) {
    
    // Evitar que podamos hacer click en una carta ya revealda
    if (card.reveal || selectedCards.length == 2) {
        return;
    }

    // Primero, siempre mostramos la carta seleccionada. Reactivamente, el estado cambia, y entonces se actualiza el DOM del template 
    card.reveal = true;

    // Añadimos la carta seleccionada al array de cartas seleccionadas
    selectedCards.push(card);

    // Si ya hemos seleccionado 2 cartas, hay que compararlas
    if (selectedCards.length == 2) {

         // hemos hecho match?
        const isMatch = selectedCards[0].id == selectedCards[1].id;
        // emitimos un evento al padre diciendo si hemos hecho match (true o false)
        emit('onCheckedCards', isMatch)

        // Si su id NO es el mismo, hemos errado. Tenemos que darle la vuelta a la cartas.
        if (selectedCards[0].id != selectedCards[1].id) {
            setTimeout(() => {
               selectedCards[0].reveal = false;
               selectedCards[1].reveal = false;
            }, 1000);           
        }
        // En cualquier caso, tenemos que 'reiniciar' el estado de la app para que podamos seleccionar las dos siguientes cartas
        setTimeout(() => {
            selectedCards = []
        },1000);
    }




    // Filtramos solo las que tienen el estado reveal
    // const cardsRevealed = cardsChessBoard.filter(card => card.reveal);
    // const numCardsRevealed = cardsRevealed.length;

    // // Hemos seleccionado un número par de cartas?
    // if (numCardsRevealed % 2 == 0) {
    //     // comprobamos la última con la penúltima
    //     console.log("cartas revelas", cardsRevealed)
    //     console.log("numero de cartas revelas", numCardsRevealed)


    //     if (cardsRevealed[numCardsRevealed - 1].id == cardsRevealed[numCardsRevealed - 2].id) {
    //         console.log("Son correctas")
    //     }
    // }
}

</script>

<template>
    <div>
        <Card @click="onCardClicked(card)" v-for="card in cardsChessBoard" :key="card.id" :back="backCardImage" :front="card.image" :reveal="card.reveal">
        </Card>
    </div>

</template>



<style scoped>
div{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
    row-gap: 1rem;
    cursor: pointer;

}
</style>