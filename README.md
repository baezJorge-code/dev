# What is this?

The github.dev web-based editor is a lightweight editing experience that runs entirely in your browser. You can navigate files and source code repositories from GitHub, and make and commit code changes.

There are two ways to go directly to a VS Code environment in your browser and start coding:

* Press the . key on any repository or pull request.
* Swap `.com` with `.dev` in the URL. For example, this repo https://github.com/github/dev becomes http://github.dev/github/dev

Preview the gif below to get a quick demo of github.dev in action.

![github dev](https://user-images.githubusercontent.com/856858/130119109-4769f2d7-9027-4bc4-a38c-10f297499e8f.gif)

# Why?
It’s a quick way to edit and navigate code. It's especially useful if you want to edit multiple files at a time or take advantage of all the powerful code editing features of Visual Studio Code when making a quick change. For more information, see our [documentation](https://github.co/codespaces-editor-help).
// server.js
const express = require("express");
const mongoose = require("mongoose");

const app = express();
app.use(express.json());

mongoose.connect("mongodb://localhost/reguladores", { useNewUrlParser: true, useUnifiedTopology: true });

const reguladorSchema = new mongoose.Schema({
    marca: String,
        numeroSerie: String,
            alimentador: String,
                potencia: Number,
                    ubicacion: { lat: Number, lng: Number },
                        mantenimiento: String
                        });

                        const Regulador = mongoose.model("Regulador", reguladorSchema);

                        app.post("/reguladores", async (req, res) => {
                            const nuevoRegulador = new Regulador(req.body);
                                await nuevoRegulador.save();
                                    res.status(201).send(nuevoRegulador);
                                    });

                                    app.get("/reguladores", async (req, res) => {
                                        const reguladores = await Regulador.find();
                                            res.send(reguladores);
                                            });

// App.js
import React, { useState, useEffect } from "react";

function App() {
    const [reguladores, setReguladores] = useState([]);
        const [nuevoRegulador, setNuevoRegulador] = useState({});

            useEffect(() => {
                    fetch("/reguladores")
                                .then((res) => res.json())
                                            .then((data) => setReguladores(data));
                                                }, []);

                                                    const agregarRegulador = async () => {
                                                            const res = await fetch("/reguladores", {
                                                                        method: "POST",
                                                                                    headers: { "Content-Type": "application/json" },
                                                                                                body: JSON.stringify(nuevoRegulador),
                                                                                                        });
                                                                                                                const data = await res.json();
                                                                                                                        setReguladores([...reguladores, data]);
                                                                                                                            };

                                                                                                                                return (
                                                                                                                                        <div>
                                                                                                                                                    <h1>Registro de Reguladores</h1>
                                                                                                                                                                {reguladores.map((r) => (
                                                                                                                                                                                <div key={r.id}>{r.marca} - {r.numeroSerie}</div>
                                                                                                                                                                                            ))}
                                                                                                                                                                                                        <button onClick={agregarRegulador}>Agregar Regulador</button>
                                                                                                                                                                                                                </div>
                                                                                                                                                                                                                    );
                                                                                                                                                                                                                    }

                                                                                                                                                                                                                    export default App;// App.js (React Native)
                                                                                                                                                                                                                    import React, { useState } from "react";
                                                                                                                                                                                                                    import { View, TextInput, Button } from "react-native";

                                                                                                                                                                                                                    function App() {
                                                                                                                                                                                                                        const [nuevoRegulador, setNuevoRegulador] = useState({});

                                                                                                                                                                                                                            const agregarRegulador = async () => {
                                                                                                                                                                                                                                    await fetch("http://tu-server.com/reguladores", {
                                                                                                                                                                                                                                                method: "POST",
                                                                                                                                                                                                                                                            headers: { "Content-Type": "application/json" },
                                                                                                                                                                                                                                                                        body: JSON.stringify(nuevoRegulador),
                                                                                                                                                                                                                                                                                });
                                                                                                                                                                                                                                                                                    };

                                                                                                                                                                                                                                                                                        return (
                                                                                                                                                                                                                                                                                                <View>
                                                                                                                                                                                                                                                                                                            <TextInput placeholder="Marca" onChangeText={(text) => setNuevoRegulador({ ...nuevoRegulador, marca: text })} />
                                                                                                                                                                                                                                                                                                                        <Button title="Registrar Regulador" onPress={agregarRegulador} />
                                                                                                                                                                                                                                                                                                                                </View>
                                                                                                                                                                                                                                                                                                                                    );
                                                                                                                                                                                                                                                                                                                                    }

                                                                                                                                                                                                                                                                                                                                    export default App;