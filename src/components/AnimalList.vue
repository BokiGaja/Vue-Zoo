<template>
    <div>
        <form action="" @submit.prevent="addAnimal">
            <h4>Add a new animal</h4>
            <input type="text" v-model="newAnimal.specie" placeholder="specie">
            <br>
            <input type="text" v-model="newAnimal.name" placeholder="name">
            <br>
            <input type="text" v-model="newAnimal.date" placeholder="date">
            <br>
            <button class="btn btn-success" type="submit">Add animal</button>
        </form>
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
                },
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
                        date: this.newAnimal.date
                    };
                    this.animals.push(newAnimal);
                    this.newAnimal.specie = '';
                    this.newAnimal.name = '';
                    this.newAnimal.date = '';
                } else {
                    alert('You must insert values to all fields')
                }
            }
        }
    }
</script>