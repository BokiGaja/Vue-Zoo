<template>
    <div>
        <form action="" @submit.prevent="addAnimal()">
            <h4>Add a new animal</h4>
            <input type="text" v-model="newAnimal.specie" placeholder="specie">
            <br>
            <input type="text" v-model="newAnimal.name" placeholder="name">
            <br>
            <input type="text" v-model="newAnimal.date" placeholder="date (MM/DD/YYYY)">
            <br>
            <select class="form-control form-control-sm" style="width: 200px; margin: auto" v-model="newAnimal.sector">
                <option v-for="sector in sectors">{{ sector }}</option>
            </select>
            <button class="btn btn-success" type="submit">Add animal</button>
        </form>
        <table class="table">
            <thead class="thread-dark">
            <tr>
                <th scope="col">#</th>
                <th scope="col">Specie</th>
                <th scope="col">Name</th>
                <th scope="col">Date of birth</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(animal, index) in animals">
                <th scope="row">{{ animals.indexOf(animal) + 1 }}</th>
                <th>{{ animal.specie }}</th>
                <td>{{ animal.name }}</td>
                <td>{{ animal.date ? animal.date : 'Unknown' }}</td>
                <button class="btn btn-primary" @click="moveAnimal(animal, index)">Move to top</button>
                <button class="btn btn-danger" @click="removeAnimal(index)">Remove</button>
            </tr>
            </tbody>
        </table>
        <table class="table table-bordered">
            <thead>
            <tr>
                <th scope="col">Sectors</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="sector in sectors">
                <button class="btn btn-info" style="margin: 5px" @click="seeAnimals(sector)">{{ sector }}</button>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    import moment from 'moment'
    export default {
        data() {
            return {
                newAnimal: {
                    specie: '',
                    name: '',
                    date: ''
                },
                animals: [
                    {specie: 'dog', name: 'Jack', date: moment('2.12.2010').format('MMMM Do YYYY'), sector: 'mammal'},
                    {specie: 'cat', name: 'Kitty', date: '', sector: 'mammal'},
                    {specie: 'fish', name: 'Nemo', date: moment('2.19.2010').format('MMMM Do YYYY'), sector: 'fish'},
                    {specie: 'snake', name: 'Samuel', date: moment('2.19.2010').format('MMMM Do YYYY'), sector: 'snake'},
                    {specie: 'snake', name: 'Poison', date: moment('2.22.2010').format('MMMM Do YYYY'), sector: 'snake'}
                ],
                sectors: ['mammal', 'fish', 'snake']
            }
        },
        methods: {
            removeAnimal(index) {
                this.animals.splice(index,1);
            },
            moveAnimal(animal, index) {
                this.animals.splice(index,1);
                this.animals.unshift(animal);
            },
            addAnimal() {
                if (this.newAnimal.specie !== '' && this.newAnimal.name !== '') {
                    const newAnimal = {
                        specie: this.newAnimal.specie,
                        name: this.newAnimal.name,
                        date: moment(this.newAnimal.date).format('MMMM Do YYYY'),
                        sector: this.newAnimal.sector
                    };
                    this.animals.push(newAnimal);
                    this.newAnimal.specie = '';
                    this.newAnimal.name = '';
                    this.newAnimal.date = '';
                    this.newAnimal.sector = '';
                } else {
                    alert('You must insert values to all fields')
                }
            },
            seeAnimals(sector) {
                let animals= [];
                this.animals.forEach(animal => {
                    if (animal.sector === sector) {
                        animals.push(animal.name);
                    }
                } );
                const animalNames = animals.join(', ');
                alert(`${sector}s: ${animalNames}`);
            }
        }
    }
</script>