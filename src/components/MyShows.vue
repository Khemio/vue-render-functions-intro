<template>
    
</template>

<script>
import { h, ref } from 'vue';


export default {
    setup(_,{slots}) {
        let inputValue = ref(null);
        let shows = ref(null);
        let error = ref(null);

        const searchText = async search => {
            if(!search) return;
            shows.value = [];
            console.log('got here', search);
            const res = await fetch(`https://api.tvmaze.com/search/shows?q=${search}`)
                .catch(e => {
                    error.value ='error' + e;
                    console.log('got error', error.value);
                    return;
                })

                shows.value = await res.json().catch(e => {error.value = e})
                console.log(shows.value)
        }

        // const slot = slots.default ? slots.default() : []
        const ss = show => (slots.sc ?  slots.sc(show): [])

        return () => h('form', {style: 'color: red; max-width: 768px; margin: auto',
            onSubmit: event => event.preventDefault()}, 
            [
                ss({shows: shows.value}),
                h('input', {onInput: event => {
                    inputValue.value = event.target.value
                    console.log(inputValue.value)
                }}),
                h('button',{
                    onClick: async () => {
                        searchText(inputValue.value)
                    }
                } ,'Press Me'),
                h('div', {class: 'shows'}, [
                    error.value ? h('div', error.value)
                    : shows.value?.map(show => 
                        h('div',{class: 'show'}, [
                            h('div', show.show.name),
                            h('img', {src: show.show.image?.medium})
                        ])
                    )
                ])
            ]
        )
    }
}

</script>

<style>
.show {
    margin: 10px;
    min-width: 210px;
}

.shows {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    justify-content: center;
}

</style>