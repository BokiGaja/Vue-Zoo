<template>
    <div>
        <form action="" @submit.prevent="addAnimal()">
            <h4>Add a new animal</h4>
            <input type="text" v-model="newAnimal.specie" placeholder="specie">
            <br>
            <input type="text" v-model="newAnimal.name" placeholder="name">
            <br>
            <input type="text" v-model="newAnimal.date" placeholder="date">
            <br>
            <select class="form-control form-control-sm" style="width: 200px; margin: auto" v-model="newAnimal.sector">
                <option v-for="sector in sectors">{{ sector }}</option>
            </select>
            <button class="btn btn-success" type="submit">Add animal</button>
        </form>
        <table class="table">
            <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Specie</th>
                <th scope="col">Name</th>
                <th scope="col">Date of birth</th>
                <th scope="col">Sector</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(animal, index) in animals">
                <th scope="row">{{ animals.indexOf(animal) + 1 }}</th>
                <th>{{ animal.specie }}</th>
                <td>{{ animal.name }}</td>
                <td>{{ animal.date ? animal.date : 'Unknown' }}</td>
                <td>{{ animal.sector }}</td>
                <button class="btn btn-primary" @click="moveAnimal(animal, index)">Move to top</button>
                <button class="btn btn-danger" @click="removeAnimal(index)">Remove</button>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                newAnimal: {
                    specie: '',
                    name: '',
                    date: '',
                    sector: ''
                },
                animals: [
                    {specie: 'dog', name: 'Jack', date: '21.12.2010', sector: 'mammal'},
                    {specie: 'cat', name: 'Kitty', date: '', sector: 'mammal'},
                    {specie: 'fish', name: 'Nemo', date: '23.12.2010', sector: 'fish'},
                    {specie: 'horse', name: 'Stud', date: '24.12.2010', sector: 'mammal'},
                    {specie: 'pig', name: 'Hans', date: '25.12.2010', sector: 'mammal'}
                ],
                sectors: ['birds', 'mammals', 'snakes']
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
                        date: this.newAnimal.date,
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
            }
        }
    }
</script>