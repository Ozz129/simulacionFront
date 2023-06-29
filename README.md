# simulacionFront, recuerden instalar axios, express, nodemon

const express = require('express');
const axios = require('axios');

const app = express();
const port = 8080;

// Ruta para consumir la API
app.get('/api', async (req, res) => {
  try {
    // Realizar una petición GET a la API
    const respuesta = await axios.get('http://localhost:3000/');

    // Obtener los datos de la respuesta
    const datos = respuesta.data;

    // Enviar los datos como respuesta al cliente
    res.json(datos);
  } catch (error) {
    // Enviar un mensaje de error al cliente
    console.log('***', error)
    res.status(500).json({ error: 'Error al consumir la API' });
  }
});

app.post('/crear', (req, res) => {

    const data  = {
        name: 'recibir el valor del input name',
        autor: 'recibir el valor del autor',
        id: 1
    }
    
    axios.post('http://localhost:3000/libros', data)
        .then((respuesta) => {
            // Manejar la respuesta de la API
            res.status(200).send(respuesta.data);
        })
        .catch((error) => {
            // Manejar cualquier error ocurrido durante la petición
            console.error('Error al hacer la petición POST:', error.message);
        });
})

app.get('/listar', async (req, res) => {
   const rta = await axios.get('http://localhost:3000/libros');

   res.status(200).send(rta.data);
})

// Iniciar el servidor
app.listen(port, () => {
  console.log(`Servidor web iniciado en el puerto ${port}`);
});
