<template>
    <section>
        <div class="jumbotron">
            <h2 class="mb-4">Formulario</h2>
            <vue-form :state="formState" @submit.prevent="enviar">
                <validate tag="div">
                    <label for="nombre">Nombre</label>
                    <input
                        type="text"
                        id="nombre"
                        class="form-control"
                        autocomplete="off"
                        v-model.trim="formData.nombre"
                        name="nombre"
                        required
                        :minlength="nombreMinLength"
                        :maxlength="nombreMaxLength"
                        no-espacios
                    />

                    <field-messages name="nombre" show="$dirty">
                        <div slot="required" class="alert alert-danger mt-1">
                            El nombre es un campo requerido
                        </div>
                        <div slot="minlength" class="alert alert-danger mt-1">
                            El nombre tiene que tener minimo
                            {{ this.nombreMinLength }} caracteres.
                        </div>
                        <div slot="maxlength" class="alert alert-danger mt-1">
                            El nombre tiene que tener maximo
                            {{ this.nombreMaxLength }} caracteres.
                        </div>
                        <div slot="no-espacios" class="alert alert-danger mt-1">
                            Ingrese su nombre sin espacios.
                        </div>
                    </field-messages>
                </validate>

                <br />

                <validate tag="div">
                    <label for="descripcion">Descripcion</label>
                    <input
                        type="text"
                        id="descripcion"
                        class="form-control"
                        v-model="formData.descripcion"
                        name="descripcion"
                        required
                    />

                    <field-messages name="descripcion" show="$dirty">
                        <div slot="required" class="alert alert-danger mt-1">
                            La descripcion es un campo requerido
                        </div>
                    </field-messages>
                </validate>

                <br />

                <validate tag="div">
                    <label for="importe">Importe</label>
                    <input
                        type="number"
                        id="importe"
                        class="form-control"
                        autocomplete="off"
                        v-model.number="formData.importe"
                        name="importe"
                        required
                    />

                    <field-messages name="importe" show="$dirty">
                        <div slot="required" class="alert alert-danger mt-1">
                            El monto a pagar es un campo requerido
                        </div>
                    </field-messages>
                </validate>

                <button
                    class="btn btn-success my-3"
                    type="submit"
                    :disabled="formState.$invalid"
                    @click="this.enviar"
                >
                    Enviar
                </button>
                <br />
            </vue-form>

            <div v-if="posts.length">
                <hr />
                <hr />
                <h2>Detalle de Gastos</h2>
                <hr />
                <label for="presupuesto">
                    <b><i>Presupuesto:</i></b>
                </label>
                <input
                    type="number"
                    id="presupuesto"
                    class="form-control"
                    style="max-width: 50%"
                    placeholder="Ingrese su presupuesto"
                    v-model.number="presupuesto"
                />
                <div class="table-responsive">
                    <table class="table">
                        <tr>
                            <th>Nombre</th>
                            <th>Descripcion</th>
                            <th>Importe</th>
                            <th>Fecha</th>
                        </tr>
                        <tr v-for="post in posts" :key="post.nombre">
                            <td>{{ post.nombre }}</td>
                            <td>{{ post.descripcion }}</td>
                            <td>{{ post.importe }}</td>
                            <td>{{ post.fecha }}</td>
                        </tr>
                        <tr v-if=" sumarDetalle >= presupuesto">
                            <td></td>
                            <td :style="{ color: this.calcularColor }">
                                TOTAL
                            </td>
                            <td  :style="{ color: this.calcularColor }"> {{ this.sumarDetalle }}</td>
                            <td></td>
                        </tr>
                        <tr v-else>
                            <td></td>
                            <td :style="{ color: presupuestoInsuficiente} ">
                                TOTAL
                            </td>
                            <td  :style="{ color: presupuestoInsuficiente} "> {{ this.sumarDetalle }}</td>
                            <td></td>
                        </tr>
                    </table>
                </div>
            </div>
            <div v-else class="alert alert-danger text-center">
                No hay datos
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: "src-components-formulario",
    props: [],
    mounted() {},
    data() {
        return {
            formState: {},
            formData: this.getDatosIniciales(),
            nombreMinLength: 3,
            nombreMaxLength: 15,
            posts: [],
            presupuesto: null,
            presupuestoInsuficiente: "#FF0000"
        };
    },
    methods: {
        getDatosIniciales() {
            return {
                nombre: null,
                descripcion: null,
                importe: null,
                fecha: null,
            };
        },
        enviar() {
            this.formData.fecha = this.getFechaAhora();
            this.posts.push(this.formData);
            this.formData = this.getDatosIniciales();
            this.formState._reset();
        },
        getFechaAhora() {
            let fecha = new Date();
            fecha =
                [
                    fecha.getMonth() + 1,
                    fecha.getDate(),
                    fecha.getFullYear(),
                ].join("/") +
                " " +
                [fecha.getHours(), fecha.getMinutes(), fecha.getSeconds()].join(
                    ":"
                );
            return fecha;
        },
    },
    computed: {
        calcularColor() { 
          let color = ""
          if (this.sumarDetalle < 1000) {
            color = "#008f39"
          } else if (this.sumarDetalle >= 1000 && this.sumarDetalle <= 5000) {
            color = "#FF00FF"
          } else if (this.sumarDetalle > 5000) {
            color = "#FF8000"
          }
          return color
        },
        sumarDetalle() {
          let suma = 0;
          this.posts.forEach(p => {
            suma += p.importe
          });
          return suma
        }

    },
};
</script>

<style scoped lang="css"></style>
