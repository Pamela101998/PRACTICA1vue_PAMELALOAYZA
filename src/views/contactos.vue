<template>
    <div>
        <h1>{{ titulo }}</h1>
        <div class="filtro">
            Filtro: <input type="search" v-model="textoBusar">
        </div>
        <br>
        <table>
            <thead>
                <tr>
                    <th>id</th>
                    <th>name</th>
                    <th>email</th>
                    <th>address</th>
                    <th>phone</th>
                    <th>country</th>
                    <th>city</th>
                    <th></th>
                </tr>
                <tr>
                    <th><input type="text" v-model="contactoNuevoObj.id"></th>
                    <th><input type="text" v-model="contactoNuevoObj.name"></th>
                    <th><input type="text" v-model="contactoNuevoObj.email"></th>
                    <th><input type="text" v-model="contactoNuevoObj.address"></th>
                    <th><input type="text" v-model="contactoNuevoObj.phone"></th>
                    <th><input type="text" v-model="contactoNuevoObj.country"></th>
                    <th><input type="text" v-model="contactoNuevoObj.city"></th>
                    <th><button @click="guardaNuevo()">Nuevo</button></th>
                </tr>
                <tr v-if="indexParaEditar !== null">
                    <th><input type="text" v-model="contactoEditarObj.id"></th>
                    <th><input type="text" v-model="contactoEditarObj.name"></th>
                    <th><input type="text" v-model="contactoEditarObj.email"></th>
                    <th><input type="text" v-model="contactoEditarObj.address"></th>
                    <th><input type="text" v-model="contactoEditarObj.phone"></th>
                    <th><input type="text" v-model="contactoEditarObj.country"></th>
                    <th><input type="text" v-model="contactoEditarObj.city"></th>
                    <th><button @click="guardaEdicion()">Guardar</button></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(contacto, index) in listaContactosComputada" :key="contacto.id">
                    <td>{{contacto.id}}</td>
                    <td>{{contacto.name}}</td>
                    <td>{{contacto.email}}</td>
                    <td>{{contacto.address}}</td>
                    <td>{{contacto.phone}}</td>
                    <td>{{contacto.country}}</td>
                    <td>{{contacto.city}}</td>
                    <td>
                        <button @click="eliminarContacto(index)">Eliminar</button>
                        <button @click="EditarContacto(contacto, index)">Editar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'MiComponente',
    data() {
        return {
            titulo: 'Agenda de Contactos',
            textoBusar: '',
            contactoNuevoObj: { 
                id: "", 
                name: "", 
                email: "", 
                address: "", 
                phone: "",
                country: "",
                city:"" 
            },
            contactoEditarObj: { 
                id: "", 
                name: "", 
                email: "", 
                address: "", 
                phone: "",
                country: "",
                city:"" 
            },  
            indexParaEditar:null, 
            contactos: [
                {id: 1, name: "Alice Johnson", email: "alice.johnson@example.com", address: "123 Maple Street", phone: "123-456-7890", country: "USA", city: "New York"},
                {id: 2, name: "Bob Smith", email: "bob.smith@example.com", address: "456 Oak Avenue", phone: "987-654-3210", country: "Canada", city: "Toronto"},
                {id: 3, name: "Carol White", email: "carol.white@example.com", address: "789 Pine Road", phone: "555-123-4567", country: "UK", city: "London"},
                {id: 4, name: "David Brown", email: "david.brown@example.com", address: "321 Elm Street", phone: "444-555-6666", country: "Australia", city: "Sydney"},
                {id: 5, name: "Emily Davis", email: "emily.davis@example.com", address: "654 Spruce Lane", phone: "333-444-5555", country: "USA", city: "Los Angeles"}
            ]
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        guardaNuevo(){
            this.contactos.push(Object.assign({}, this.contactoNuevoObj));
        },
        eliminarContacto(index){
            this.contactos.splice(index,1);
        },
        guardaEdicion(){
            this.contactos[this.indexParaEditar] = Object.assign({},this.contactoEditarObj);
            this.indexParaEditar = null;
        },
        EditarContacto(contacto, index){
            this.indexParaEditar = index;
            this.contactoEditarObj = Object.assign({},contacto);
        }
    },
    computed: {
        listaContactosComputada(){
            return this.contactos.filter(item => item.name.toLowerCase().includes(this.textoBusar.toLowerCase())||item.email.toLowerCase().includes(this.textoBusar.toLowerCase()));
        } 
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script >

<style scope>
h1 {
    color: #42b983;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
}
th {
    background-color: #f2f2f2;
    text-align: left;
}
</style>