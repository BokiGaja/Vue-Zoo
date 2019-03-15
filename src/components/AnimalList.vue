<template>
    <div class="container">
        <form @submit.prevent="addAnimal">
            <h4>Add a new animal</h4>
            <input type="text" v-model="animal.specie" placeholder="specie" required>
            <br>
            <input type="text" v-model="animal.name" placeholder="name" required>
            <br>
            <input type="text" v-model="animal.birthDate" placeholder="date (MM/DD/YYYY)">
            <br>
            <select class="form-control form-control-sm" style="width: 210px; margin: auto" v-model="animal.sector">
                <option v-for="sector in sectors" :key="sector" :value="sector">{{ sector }}</option>
            </select>
            <button class="btn btn-success" type="submit" style="margin: 5px;">Add animal</button>
        </form>
        <table class="table">
            <thead class="thead-dark">
            <tr>
                <th scope="col">#</th>
                <th scope="col">Specie</th>
                <th scope="col">Name</th>
                <th scope="col">Date of birth</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(animal, index) in animals" :key="index">
                <th scope="row">{{ (index+1) }}</th>
                <th>{{ animal.specie }}</th>
                <td>{{ animal.name }}</td>
                <td>{{ animal.birthDate || 'Unknown' }}</td>
                <button class="btn btn-primary" @click="moveAnimal(index)">Move to top</button>
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
                animal: {
                    specie: '',
                    name: '',
                    birthDate: '',
                    sector: ''
                },
                animals: [
                    {specie: 'dog', name: 'Jack', birthDate: moment('2.12.2010').format('MMMM Do YYYY'), sector: 'mammal'},
                    {specie: 'cat', name: 'Kitty', birthDate: '', sector: 'mammal'},
                    {specie: 'fish', name: 'Nemo', birthDate: moment('2.19.2010').format('MMMM Do YYYY'), sector: 'fish'},
                    {specie: 'snake', name: 'Samuel', birthDate: moment('2.19.2010').format('MMMM Do YYYY'), sector: 'snake'},
                    {specie: 'snake', name: 'Poison', birthDate: moment('2.22.2010').format('MMMM Do YYYY'), sector: 'snake'}
                ],
                sectors: ['mammal', 'fish', 'snake']
            }
        },

        methods: {

            removeAnimal(index) {
                this.animals.splice(index,1);
            },

            moveAnimal(index) {
                this.animals.unshift(this.animals[index]);
                this.animals.splice(index+1,1);
            },

            clearAnimalObj() {
                this.animal.specie = '';
                this.animal.name = '';
                this.animal.birthDate = '';
                this.animal.sector = '';
            },

            addAnimal() {
                    this.animals.push({...this.animal});
                    this.clearAnimalObj();
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