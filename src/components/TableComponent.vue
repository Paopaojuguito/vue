<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-3">

            </div>
            <div class="col-md-6">
                <table class="table">
                    <thead>
                        <tr>
                            <th>Id</th>
                            <th>Contact</th>
                            <th>Phone</th>
                            <th>Date added</th>
                            <th>Status</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(row, index) in data" :key="row.id" v-bind:class="{'table-active' : index%2 == 0}"> <!--color de filamintercalado-->
                            <td>
                                {{ row.id }}
                            </td>
                            <td>
                                {{ row.contact }}
                            </td>
                            <td>
                                {{ row.phone }}
                            </td>
                            <td>
                                {{ row.date }}
                            </td>
                            <td>
                                {{ row.status }}
                            </td>
                            <td>
                                <button type="button" class="btn btn-success btn-sm" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="Updaterow(index)"> <!--hacer que se active el metodo select-->
                                    Update
                                </button>
                                <button type="button" class="btn btn-danger btn-sm" @click="remove(index)">
                                    Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="col-mod-3">
                <button type="button" class="btn btn-primary btn-sm" @click="create()">
                    Create
                </button>
            </div>
        </div>
    </div>

    <!--Modal (Notificacion flotante)-->
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-12">
                <div class="row">
                    <div class="col-md-3">
                    </div>
                    <div class="col-md-6">
                        <!-- Boton para abrir modal -->
                        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
                            Add Contact
                        </button>

                        <!-- Modal -->
                        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                            <div class="modal-dialog">
                                <div class="modal-content">
                                    <div class="modal-header"> <!--encabezado del modal-->
                                        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                                    </div>
                                    <div class="modal-body"> <!--cuerpo del modal-->
                                        <div class="mb-3">
                                            <label for="exampleFormControlInput1" class="form-label">Id</label>
                                            <input type="text" class="form-control" id="" placeholder="id" v-model="inputId">  <!--Nombre variable-->

                                            <label for="exampleFormControlInput1" class="form-label">Contact</label>
                                            <input type="text" class="form-control" id="" placeholder="Contact" v-model="inputContact">

                                            <label for="exampleFormControlInput1" class="form-label">Phone</label>
                                            <input type="text" class="form-control" id="" placeholder="Phone" v-model="inputPhone">

                                            <label for="exampleFormControlInput1" class="form-label">Date</label>
                                            <input type="date" class="form-control" id="" placeholder="Date" v-model="inputDate">

                                            <label for="exampleFormControlInput1" class="form-label">Status</label>
                                            <input type="text" class="form-control" id="" placeholder="Status" v-model="inputStatus">

                                        </div>
                                    </div>
                                    <div class="modal-footer"> <!--botones inferiores del modal-->
                                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                                        <button type="button" class="btn btn-primary" @click="saveChanges()">Save changes</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                    </div>
                    <div class="col-md-3">
                    </div>
                </div>
            </div>
        </div>
	</div>
</template>

<script>
    export default{
        data(){
            return{
                data : [
                    {id: 1, contact: "Veronica", phone: "4492040303", date: "12/07/2022", status: "Activo"},
                    {id: 2, contact: "Armando", phone: "4492040304", date: "13/07/2022", status: "Activo"},
                    {id: 3, contact: "Ceci", phone: "4492040305", date: "14/07/2022", status: "No Activo"},
                    {id: 4, contact: "Fernando", phone: "4492040306", date: "15/07/2022", status: "Activo"},
                    {id: 5, contact: "Lili", phone: "4492040307", date: "16/07/2022", status: "Activo"}
                ],
                inputId : "",
                inputContact : "", 
                inputPhone : "",   
                inputDate : "",
                inputStatus : "",       
            
            }
        },
        methods:{
            select(id, index){
                console.log("Rowid = " + id);
                console.log("Index = " + index);

                console.log(this.data[index].contact); /*Imprimir dato */
                this.data[index].contact="Rodrigo"; /*Modificar dato */
                console.log(this.data[index].contact); /*Mostrar nuevo dato */
            },
            remove(index){
                console.log(index);
                this.data.splice(index, 1);
            },
            create(){ /*dato estatico*/
                this.data.push({id: 6, contact: "Ana", phone: "4492040308", date: "17/07/2022", status: "Activo"});
            },
            saveChanges(){ /*Metodo para guardar datos no estaticos (guardarlos desde el modal siempre y cuando no este vacio)*/
                if (this.inputId !="" && this.inputContact !="" && this.inputPhone !="" && this.inputDate !="" && this.inputStatus) {
                this.data.push({id: this.inputId, contact: this.inputContact, phone: this.inputPhone, date: this.inputDate, status: this.inputStatus});
                this.inputId = "";
                this.inputContact = "";
                this.inputPhone = "";  
                this.inputDate = "";
                this.inputStatus = ""; 
                } else{
                    alert("All fields are requiered")
                }
            },
            Updaterow(index){
                this.inputId = this.data[index].id;
                this.inputContact = this.data[index].contact;
                this.inputPhone = this.data[index].phone;   
                this.inputDate = this.data[index].date;
                this.inputStatus = this.data[index].status;
            }
        }
    }

</script>