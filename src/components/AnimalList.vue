<template>
    <table class="table">
        <thead>
        <tr>
            <th scope="col">#</th>
            <th scope="col">Specie</th>
            <th scope="col">Name</th>
            <th scope="col">Date of birth</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="animal in animals" @click="removeAnimal(animals.indexOf(animal))">
            <th scope="row">{{ animals.indexOf(animal) + 1 }}</th>
            <td>{{ animal.specie }}</td>
            <td>{{ animal.name }}</td>
            <td>{{ animal.date ? animal.date : 'Unknown' }}</td>
        </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        data() {
            return {
                animals: [
                    {specie: 'dog', name: 'Jack', date: '21.12.2010'},
                    {specie: 'cat', name: 'Kitty', date: ''},
                    {specie: 'fish', name: 'Nemo', date: '23.12.2010'},
                    {specie: 'horse', name: 'Stud', date: '24.12.2010'},
                    {specie: 'pig', name: 'Hans', date: '25.12.2010'}
                ]
            }
        },
        methods: {
            removeAnimal(index) {
                this.animals.splice(index,1);
            }
        }
    }
</script>