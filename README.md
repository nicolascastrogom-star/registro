<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registro de Asistencia</title>
  <style>
    body { font-family: sans-serif; background-color: #f0f2f5; padding: 20px; display: flex; justify-content: center; }
    .card { background: white; padding: 25px; border-radius: 10px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); width: 100%; max-width: 400px; }
    h2 { text-align: center; color: #1a73e8; margin-top: 0; }
    label { display: block; margin-top: 12px; font-weight: bold; color: #333; }
    input { width: 100%; padding: 12px; margin-top: 5px; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box; font-size: 16px; }
    button { width: 100%; padding: 14px; margin-top: 20px; background-color: #1a73e8; color: white; border: none; border-radius: 6px; font-size: 16px; font-weight: bold; cursor: pointer; }
    button:disabled { background-color: #cccccc; }
    #msg { margin-top: 15px; font-weight: bold; text-align: center; }
  </style>
</head>
<body>

<div class="card">
  <h2>Registro de Asistencia</h2>
  <form id="registroForm">
    <label for="nombre">Nombre Completo:</label>
    <input type="text" id="nombre" required placeholder="Ej. Juan Pérez">

    <label for="email">Correo Electrónico:</label>
    <input type="email" id="email" required placeholder="ejemplo@correo.com">

    <label for="telefono">Teléfono:</label>
    <input type="tel" id="telefono" required placeholder="Ej. 3001234567">

    <button type="submit" id="btnSubmit">Enviar Registro</button>
  </form>
  <div id="msg"></div>
</div>

<script>
  // ATENCIÓN: Reemplaza la URL de abajo por tu URL de Google Apps Script (la que termina en /exec)
  const SCRIPT_URL = 'TU_URL_DE_APPS_SCRIPT_AQUI';

  document.getElementById('registroForm').addEventListener('submit', function(e) {
    e.preventDefault();
    
    const btn = document.getElementById('btnSubmit');
    const msg = document.getElementById('msg');
    btn.disabled = true;
    msg.style.color = "black";
    msg.innerText = "Guardando...";

    const payload = {
      nombre: document.getElementById('nombre').value,
      email: document.getElementById('email').value,
      telefono: document.getElementById('telefono').value
    };

    fetch(SCRIPT_URL, {
      method: 'POST',
      mode: 'no-cors',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(payload)
    })
    .then(() => {
      msg.style.color = "green";
      msg.innerText = "¡Registro exitoso!";
      document.getElementById('registroForm').reset();
      btn.disabled = false;
    })
    .catch(error => {
      msg.style.color = "red";
      msg.innerText = "Error al guardar los datos.";
      console.error(error);
      btn.disabled = false;
    });
  });
</script>

</body>
</html>
