<?php
session_start();

/* =========================
   CONEXIÓN MYSQL
========================= */

$conn = new mysqli("localhost","root","");
$conn->query("CREATE DATABASE IF NOT EXISTS comedor_comunitario");
$conn->select_db("comedor_comunitario");
$conn->set_charset("utf8");

/* =========================
   TABLAS
========================= */

$conn->query("
CREATE TABLE IF NOT EXISTS admin(
  id INT AUTO_INCREMENT PRIMARY KEY,
  usuario VARCHAR(50),
  password VARCHAR(255)
)");

$conn->query("
CREATE TABLE IF NOT EXISTS beneficiarios(
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  telefono VARCHAR(50),
  direccion VARCHAR(255),
  fecha_registro DATETIME DEFAULT NOW()
)");

$conn->query("
CREATE TABLE IF NOT EXISTS voluntarios(
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  telefono VARCHAR(50),
  dias VARCHAR(100),
  fecha_registro DATETIME DEFAULT NOW()
)");

$conn->query("
CREATE TABLE IF NOT EXISTS donaciones(
  id INT AUTO_INCREMENT PRIMARY KEY,
  donante VARCHAR(100),
  tipo VARCHAR(100),
  monto VARCHAR(50),
  fecha_registro DATETIME DEFAULT NOW()
)");

$conn->query("
CREATE TABLE IF NOT EXISTS alimentos(
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  dia VARCHAR(100),
  cantidad VARCHAR(50),
  fecha_registro DATETIME DEFAULT NOW()
)");

$conn->query("
CREATE TABLE IF NOT EXISTS usuarios(
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  password VARCHAR(255),
  tipo ENUM('beneficiario','voluntario','donante'),
  telefono VARCHAR(50),
  direccion VARCHAR(255),
  dias VARCHAR(100),
  monto_donacion VARCHAR(50),
  fecha_registro DATETIME DEFAULT NOW()
)");

$conn->query("
CREATE TABLE IF NOT EXISTS quejas_sugerencias(
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  email VARCHAR(100),
  tipo ENUM('queja','sugerencia'),
  mensaje TEXT,
  fecha DATETIME DEFAULT NOW()
)");

/* =========================
   ADMIN DEFAULT
========================= */
$check = $conn->query("SELECT * FROM admin");
if($check->num_rows == 0){
  $pass = md5("admin123");
  $conn->query("INSERT INTO admin(usuario,password) VALUES('admin','$pass')");
}

/* =========================
   CORREO - PHPMailer simple vía mail()
========================= */
function enviarCorreo($para, $asunto, $cuerpo){
  $headers  = "MIME-Version: 1.0\r\n";
  $headers .= "Content-Type: text/html; charset=UTF-8\r\n";
  $headers .= "From: Comedor Comunitario <noreply@comedorcomunitario.com>\r\n";
  $headers .= "Reply-To: noreply@comedorcomunitario.com\r\n";
  $cuerpoHtml = "
  <div style='font-family:Arial;max-width:600px;margin:auto;border:1px solid #ddd;border-radius:10px;overflow:hidden;'>
    <div style='background:#2d6a4f;padding:20px;text-align:center;'>
      <h2 style='color:white;margin:0;'>Comedor Comunitario</h2>
    </div>
    <div style='padding:30px;'>
      $cuerpo
    </div>
    <div style='background:#f4f4f4;padding:15px;text-align:center;font-size:13px;color:#888;'>
      Comedor Comunitario © 2026 | Este es un correo automático
    </div>
  </div>";
  return @mail($para, $asunto, $cuerpoHtml, $headers);
}

/* =========================
   LOGIN ADMIN
========================= */
if(isset($_POST['login'])){
  $usuario  = $conn->real_escape_string($_POST['usuario']);
  $password = md5($_POST['password']);
  $sql = $conn->query("SELECT * FROM admin WHERE usuario='$usuario' AND password='$password'");
  if($sql->num_rows > 0){
    $_SESSION['admin'] = true;
    header("Location:index.php?admin&seccion=dashboard");
    exit;
  } else {
    $error_login = "Usuario o contraseña incorrectos.";
  }
}

/* =========================
   LOGIN USUARIO
========================= */
if(isset($_POST['login_usuario'])){
  $email    = $conn->real_escape_string($_POST['email']);
  $password = md5($_POST['password']);
  $sql = $conn->query("SELECT * FROM usuarios WHERE email='$email' AND password='$password'");
  if($sql->num_rows > 0){
    $u = $sql->fetch_assoc();
    $_SESSION['usuario'] = $u;
    header("Location:index.php?micuenta");
    exit;
  } else {
    $error_login_u = "Email o contraseña incorrectos.";
  }
}

/* =========================
   REGISTRO USUARIO
========================= */
if(isset($_POST['registrar_usuario'])){
  $nombre   = $conn->real_escape_string($_POST['nombre']);
  $email    = $conn->real_escape_string($_POST['email']);
  $password = md5($_POST['password']);
  $tipo     = $conn->real_escape_string($_POST['tipo']);
  $telefono = $conn->real_escape_string($_POST['telefono'] ?? '');
  $direccion= $conn->real_escape_string($_POST['direccion'] ?? '');
  $dias     = $conn->real_escape_string($_POST['dias'] ?? '');
  $monto    = $conn->real_escape_string($_POST['monto_donacion'] ?? '');

  $existe = $conn->query("SELECT id FROM usuarios WHERE email='$email'");
  if($existe->num_rows > 0){
    $error_registro = "Ese correo ya está registrado.";
  } else {
    $conn->query("INSERT INTO usuarios(nombre,email,password,tipo,telefono,direccion,dias,monto_donacion)
                  VALUES('$nombre','$email','$password','$tipo','$telefono','$direccion','$dias','$monto')");

    // Guardar también en la tabla correspondiente
    if($tipo == 'beneficiario'){
      $conn->query("INSERT INTO beneficiarios(nombre,telefono,direccion) VALUES('$nombre','$telefono','$direccion')");
    } elseif($tipo == 'voluntario'){
      $conn->query("INSERT INTO voluntarios(nombre,telefono,dias) VALUES('$nombre','$telefono','$dias')");
    } elseif($tipo == 'donante'){
      $conn->query("INSERT INTO donaciones(donante,tipo,monto) VALUES('$nombre','Donación Inicial','$monto')");
    }

    // Correo de bienvenida
    $cuerpoCorreo = "<h3>¡Bienvenido/a, $nombre!</h3>
    <p>Tu cuenta ha sido creada exitosamente como <b>$tipo</b>.</p>
    <p>Gracias por unirte a nuestra comunidad. Juntos hacemos la diferencia.</p>
    <p>Puedes iniciar sesión con tu correo: <b>$email</b></p>";
    enviarCorreo($email, "Bienvenido al Comedor Comunitario", $cuerpoCorreo);

    $registro_ok = "¡Registro exitoso! Ya puedes iniciar sesión.";
  }
}

/* =========================
   GUARDAR BENEFICIARIO (ADMIN)
========================= */
if(isset($_POST['guardar_beneficiario'])){
  $n = $conn->real_escape_string($_POST['nombre']);
  $t = $conn->real_escape_string($_POST['telefono']);
  $d = $conn->real_escape_string($_POST['direccion']);
  $conn->query("INSERT INTO beneficiarios(nombre,telefono,direccion) VALUES('$n','$t','$d')");
  header("Location:index.php?admin&seccion=beneficiarios"); exit;
}

/* =========================
   GUARDAR VOLUNTARIO (ADMIN)
========================= */
if(isset($_POST['guardar_voluntario'])){
  $n = $conn->real_escape_string($_POST['nombre']);
  $t = $conn->real_escape_string($_POST['telefono']);
  $d = $conn->real_escape_string($_POST['dias']);
  $conn->query("INSERT INTO voluntarios(nombre,telefono,dias) VALUES('$n','$t','$d')");
  header("Location:index.php?admin&seccion=voluntarios"); exit;
}

/* =========================
   GUARDAR DONACION (ADMIN)
========================= */
if(isset($_POST['guardar_donacion'])){
  $d = $conn->real_escape_string($_POST['donante']);
  $t = $conn->real_escape_string($_POST['tipo']);
  $m = $conn->real_escape_string($_POST['monto']);
  $conn->query("INSERT INTO donaciones(donante,tipo,monto) VALUES('$d','$t','$m')");
  header("Location:index.php?admin&seccion=donaciones"); exit;
}

/* =========================
   GUARDAR ALIMENTO (ADMIN)
========================= */
if(isset($_POST['guardar_alimento'])){
  $n = $conn->real_escape_string($_POST['nombre']);
  $d = $conn->real_escape_string($_POST['dia']);
  $c = $conn->real_escape_string($_POST['cantidad']);
  $conn->query("INSERT INTO alimentos(nombre,dia,cantidad) VALUES('$n','$d','$c')");
  header("Location:index.php?admin&seccion=alimentos"); exit;
}

/* =========================
   EDITAR REGISTROS
========================= */
if(isset($_POST['editar_registro'])){
  $id    = intval($_POST['id']);
  $tabla = $conn->real_escape_string($_POST['tabla']);
  $campos = [];
  unset($_POST['editar_registro'], $_POST['id'], $_POST['tabla']);
  foreach($_POST as $campo => $valor){
    $c = $conn->real_escape_string($campo);
    $v = $conn->real_escape_string($valor);
    $campos[] = "$c='$v'";
  }
  if(!empty($campos)){
    $set = implode(",", $campos);
    $conn->query("UPDATE $tabla SET $set WHERE id=$id");
  }
  $seccion = ['beneficiarios'=>'beneficiarios','voluntarios'=>'voluntarios','donaciones'=>'donaciones','alimentos'=>'alimentos'][$tabla] ?? 'dashboard';
  header("Location:index.php?admin&seccion=$seccion"); exit;
}

/* =========================
   ELIMINAR
========================= */
if(isset($_GET['eliminar'])){
  $id    = intval($_GET['id']);
  $tabla = $conn->real_escape_string($_GET['tabla']);
  $conn->query("DELETE FROM $tabla WHERE id=$id");
  $seccion = $_GET['seccion'] ?? 'dashboard';
  header("Location:index.php?admin&seccion=$seccion"); exit;
}

/* =========================
   QUEJAS Y SUGERENCIAS
========================= */
if(isset($_POST['enviar_queja'])){
  $nombre  = $conn->real_escape_string($_POST['nombre']);
  $email   = $conn->real_escape_string($_POST['email']);
  $tipo    = $conn->real_escape_string($_POST['tipo']);
  $mensaje = $conn->real_escape_string($_POST['mensaje']);
  $conn->query("INSERT INTO quejas_sugerencias(nombre,email,tipo,mensaje) VALUES('$nombre','$email','$tipo','$mensaje')");

  // Enviar correo al administrador
  $cuerpoAdmin = "
  <h3>Nueva $tipo recibida</h3>
  <table style='width:100%;border-collapse:collapse;'>
    <tr><td style='padding:8px;border:1px solid #ddd;'><b>Nombre:</b></td><td style='padding:8px;border:1px solid #ddd;'>$nombre</td></tr>
    <tr><td style='padding:8px;border:1px solid #ddd;'><b>Correo:</b></td><td style='padding:8px;border:1px solid #ddd;'>$email</td></tr>
    <tr><td style='padding:8px;border:1px solid #ddd;'><b>Tipo:</b></td><td style='padding:8px;border:1px solid #ddd;'>".ucfirst($tipo)."</td></tr>
    <tr><td style='padding:8px;border:1px solid #ddd;'><b>Mensaje:</b></td><td style='padding:8px;border:1px solid #ddd;'>$mensaje</td></tr>
  </table>";
  enviarCorreo("21alexaaguilar@gmail.com", "Nueva $tipo - Comedor Comunitario", $cuerpoAdmin);

  // Confirmar al usuario
  if(!empty($email)){
    $cuerpoUser = "<h3>Gracias por contactarnos</h3>
    <p>Hemos recibido tu <b>$tipo</b>. Nos pondremos en contacto contigo pronto.</p>
    <p><b>Tu mensaje:</b> $mensaje</p>";
    enviarCorreo($email, "Recibimos tu $tipo - Comedor Comunitario", $cuerpoUser);
  }
  $queja_ok = "¡Mensaje enviado correctamente!";
}

/* =========================
   EXPORTAR PDF (admin)
========================= */
if(isset($_GET['exportar_pdf'])){
  $tabla   = $_GET['tabla'] ?? 'beneficiarios';
  $tablas_validas = ['beneficiarios','voluntarios','donaciones','alimentos','usuarios','quejas_sugerencias'];
  if(!in_array($tabla, $tablas_validas)) die("Tabla no válida");

  $resultado = $conn->query("SELECT * FROM $tabla");
  $filas = [];
  while($r = $resultado->fetch_assoc()) $filas[] = $r;

  $fecha = date("d/m/Y H:i");
  $html_tabla = "";
  if(!empty($filas)){
    $html_tabla .= "<tr>";
    foreach(array_keys($filas[0]) as $col) $html_tabla .= "<th>".htmlspecialchars(strtoupper($col))."</th>";
    $html_tabla .= "</tr>";
    foreach($filas as $fila){
      $html_tabla .= "<tr>";
      foreach($fila as $val) $html_tabla .= "<td>".htmlspecialchars($val)."</td>";
      $html_tabla .= "</tr>";
    }
  }

  $nombreTabla = ucfirst(str_replace('_',' ',$tabla));

  echo '<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Reporte '.$nombreTabla.'</title>
<style>
  body{font-family:Arial;padding:30px;color:#222;}
  .encabezado{display:flex;justify-content:space-between;align-items:center;border-bottom:3px solid #2d6a4f;padding-bottom:15px;margin-bottom:20px;}
  .encabezado h1{color:#2d6a4f;font-size:22px;margin:0;}
  .encabezado p{margin:0;font-size:13px;color:#666;}
  .empresa{font-size:12px;color:#888;margin-bottom:20px;}
  h2{color:#2d6a4f;font-size:18px;margin-bottom:10px;}
  table{width:100%;border-collapse:collapse;margin-top:10px;font-size:13px;}
  th{background:#2d6a4f;color:white;padding:8px;}
  td{border:1px solid #ddd;padding:7px;text-align:center;}
  tr:nth-child(even){background:#f9f9f9;}
  .footer{margin-top:30px;text-align:center;font-size:12px;color:#888;border-top:1px solid #ddd;padding-top:10px;}
  .stats{display:flex;gap:20px;margin-bottom:20px;}
  .stat-box{background:#f0f9f4;border:1px solid #2d6a4f;border-radius:8px;padding:12px 20px;text-align:center;}
  .stat-box span{font-size:24px;font-weight:bold;color:#2d6a4f;display:block;}
  .stat-box small{color:#555;font-size:12px;}
  @media print{.no-print{display:none;}}
</style>
</head>
<body>

<div class="encabezado">
  <div>
    <h1>&#127859; Comedor Comunitario</h1>
    <p>Calle Principal #123 | Tel: 4420000000 | comedor@gmail.com</p>
  </div>
  <div style="text-align:right;">
    <p><b>Reporte Generado:</b><br>'.$fecha.'</p>
  </div>
</div>

<div class="empresa">
  <b>REPORTE OFICIAL</b> &mdash; Este documento es generado automáticamente por el sistema de gestión del Comedor Comunitario.<br>
  Para más información comuníquese al correo comedor@gmail.com
</div>

<h2>Reporte de: '.$nombreTabla.'</h2>

<div class="stats">
  <div class="stat-box">
    <span>'.count($filas).'</span>
    <small>Total de registros</small>
  </div>
  <div class="stat-box">
    <span>'.$fecha.'</span>
    <small>Fecha de exportación</small>
  </div>
</div>

<table>
  '.$html_tabla.'
</table>

<div class="footer">
  Comedor Comunitario &copy; 2026 &mdash; Documento generado el '.$fecha.'<br>
  Este reporte es confidencial y de uso interno.
</div>

<br>
<div class="no-print" style="text-align:center;">
  <button onclick="window.print()" style="background:#2d6a4f;color:white;padding:10px 25px;border:none;border-radius:8px;cursor:pointer;font-size:16px;margin-right:10px;">
    🖨️ Imprimir / Guardar PDF
  </button>
  <button onclick="window.close()" style="background:#888;color:white;padding:10px 25px;border:none;border-radius:8px;cursor:pointer;font-size:16px;">
    Cerrar
  </button>
</div>

<script>
// Auto-prompt print
// window.onload = () => window.print();
</script>
</body>
</html>';
  exit;
}

/* =========================
   EXPORTAR EXCEL (CSV)
========================= */
if(isset($_GET['exportar_excel'])){
  $tabla = $_GET['tabla'] ?? 'beneficiarios';
  $tablas_validas = ['beneficiarios','voluntarios','donaciones','alimentos','usuarios','quejas_sugerencias'];
  if(!in_array($tabla, $tablas_validas)) die("Tabla no válida");

  $resultado = $conn->query("SELECT * FROM $tabla");
  $filas = [];
  while($r = $resultado->fetch_assoc()) $filas[] = $r;

  header('Content-Type: text/csv; charset=utf-8');
  header('Content-Disposition: attachment; filename="reporte_'.strtolower($tabla).'_'.date('Y-m-d').'.csv"');
  $output = fopen('php://output','w');
  fprintf($output, chr(0xEF).chr(0xBB).chr(0xBF)); // BOM UTF-8

  // Info empresa
  fputcsv($output, ["COMEDOR COMUNITARIO - Reporte: ".strtoupper($tabla)]);
  fputcsv($output, ["Fecha de exportación:", date("d/m/Y H:i")]);
  fputcsv($output, ["Correo:", "comedor@gmail.com"]);
  fputcsv($output, ["Teléfono:", "4420000000"]);
  fputcsv($output, [""]);

  if(!empty($filas)){
    fputcsv($output, array_keys($filas[0]));
    foreach($filas as $fila) fputcsv($output, $fila);
  }
  fputcsv($output, [""]);
  fputcsv($output, ["Total de registros:", count($filas)]);
  fputcsv($output, ["Generado por:", "Sistema Comedor Comunitario"]);
  fclose($output);
  exit;
}

/* =========================
   ENVIAR REPORTE POR CORREO
========================= */
if(isset($_POST['enviar_reporte_correo'])){
  $tabla      = $conn->real_escape_string($_POST['tabla_reporte']);
  $destinatario = $conn->real_escape_string($_POST['correo_destino']);
  $tablas_validas = ['beneficiarios','voluntarios','donaciones','alimentos','usuarios','quejas_sugerencias'];

  if(in_array($tabla, $tablas_validas) && filter_var($destinatario, FILTER_VALIDATE_EMAIL)){
    $resultado = $conn->query("SELECT * FROM $tabla");
    $filas = []; while($r = $resultado->fetch_assoc()) $filas[] = $r;
    $nombreTabla = ucfirst(str_replace('_',' ',$tabla));
    $fecha = date("d/m/Y H:i");

    $html_tabla_email = "<table style='width:100%;border-collapse:collapse;font-size:13px;'>";
    if(!empty($filas)){
      $html_tabla_email .= "<tr>";
      foreach(array_keys($filas[0]) as $col)
        $html_tabla_email .= "<th style='background:#2d6a4f;color:white;padding:6px;'>".htmlspecialchars(strtoupper($col))."</th>";
      $html_tabla_email .= "</tr>";
      foreach($filas as $fila){
        $html_tabla_email .= "<tr>";
        foreach($fila as $val) $html_tabla_email .= "<td style='border:1px solid #ddd;padding:5px;text-align:center;'>".htmlspecialchars($val)."</td>";
        $html_tabla_email .= "</tr>";
      }
    }
    $html_tabla_email .= "</table>";

    $cuerpo = "
    <h2>Reporte de $nombreTabla</h2>
    <p><b>Generado el:</b> $fecha</p>
    <p><b>Total de registros:</b> ".count($filas)."</p>
    <br>
    $html_tabla_email
    <br>
    <p style='font-size:12px;color:#888;'>Este reporte fue generado y enviado automáticamente por el sistema del Comedor Comunitario.</p>";

    $ok = enviarCorreo($destinatario, "Reporte de $nombreTabla - Comedor Comunitario", $cuerpo);
    $reporte_correo_ok = $ok ? "✅ Reporte enviado a $destinatario" : "⚠️ No se pudo enviar (configura SMTP en producción)";
  } else {
    $reporte_correo_ok = "❌ Datos inválidos.";
  }
}

/* =========================
   CERRAR SESIÓN
========================= */
if(isset($_GET['logout'])){
  session_destroy();
  header("Location:index.php"); exit;
}

$seccion_admin = $_GET['seccion'] ?? 'dashboard';
?>
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Comedor Comunitario</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial;}
html{scroll-behavior:smooth;}
body{background:#fffdf6;}

/* HEADER */
header{display:flex;justify-content:space-between;align-items:center;padding:15px 40px;background:white;box-shadow:0 2px 10px rgba(0,0,0,.1);position:sticky;top:0;z-index:1000;}
.logo{display:flex;align-items:center;gap:15px;}
.logo img{width:90px;height:90px;object-fit:contain;}
nav a{margin:0 12px;text-decoration:none;font-weight:bold;color:#2d6a4f;font-size:17px;}
nav a:hover{color:#ff8c42;}

/* DROPDOWN */
.dropdown{position:relative;display:inline-block;}
.dropdown-btn{background:none;border:none;font-weight:bold;color:#2d6a4f;font-size:17px;cursor:pointer;padding:0 12px;}
.dropdown-btn:hover{color:#ff8c42;}
.dropdown-content{display:none;position:absolute;right:0;background:white;min-width:200px;box-shadow:0 5px 15px rgba(0,0,0,.15);border-radius:10px;z-index:2000;padding:10px 0;}
.dropdown-content a{display:block;padding:10px 20px;color:#2d6a4f;text-decoration:none;font-weight:bold;}
.dropdown-content a:hover{background:#f0f9f4;color:#ff8c42;}
.dropdown:hover .dropdown-content{display:block;}

/* CARRUSEL */
.carrusel{position:relative;height:500px;overflow:hidden;}
.slide{display:none;position:absolute;width:100%;height:100%;}
.slide.active{display:block;}
.slide img{width:100%;height:500px;object-fit:cover;}
.texto{position:absolute;bottom:40px;left:40px;background:rgba(0,0,0,.5);padding:15px 20px;border-radius:10px;color:white;font-size:30px;}

/* INTRO */
.intro{padding:60px;text-align:center;}
.intro h1{color:#2d6a4f;margin-bottom:20px;font-size:50px;}
.intro p{font-size:20px;line-height:35px;max-width:900px;margin:auto;}

/* LINKS INICIO */
.inicio-links{display:flex;justify-content:center;gap:20px;margin:30px 0 10px;}
.inicio-links a{text-decoration:none;font-size:17px;font-weight:bold;color:#2d6a4f;border:2px solid #2d6a4f;padding:12px 28px;border-radius:30px;transition:.3s;}
.inicio-links a:hover{background:#2d6a4f;color:white;}

/* GALERIA */
.galeria{padding:40px;}
.galeria h2{text-align:center;margin-bottom:30px;color:#2d6a4f;font-size:40px;}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;}
.grid img{width:100%;height:250px;object-fit:cover;border-radius:15px;}

/* CONTACTO */
.contacto{padding:50px;background:#f4f4f4;margin-top:50px;}
.contacto-container{display:flex;justify-content:space-between;align-items:flex-start;gap:40px;flex-wrap:wrap;}
.info-contacto{flex:1;min-width:300px;}
.contacto h2{margin-bottom:20px;color:#2d6a4f;font-size:40px;}
.contacto p{font-size:18px;margin:12px 0;}

/* QUEJAS Y SUGERENCIAS */
.quejas-section{flex:1;min-width:300px;}
.quejas-section h2{margin-bottom:20px;color:#2d6a4f;font-size:40px;}
.quejas-form input,
.quejas-form select,
.quejas-form textarea{width:100%;padding:12px;margin:8px 0;font-size:16px;border:1px solid #ccc;border-radius:8px;}
.quejas-form textarea{height:100px;resize:vertical;}

/* FOOTER */
footer{background:#2d6a4f;color:white;text-align:center;padding:20px;font-size:18px;}

/* BOTONES */
.btn{background:#ff8c42;padding:11px 20px;border:none;border-radius:10px;color:white;cursor:pointer;text-decoration:none;display:inline-block;margin-top:8px;font-size:17px;}
.btn:hover{background:#ff7a21;}
.btn-verde{background:#2d6a4f;}
.btn-verde:hover{background:#245c43;}
.btn-rojo{background:#e74c3c;}
.btn-rojo:hover{background:#c0392b;}
.btn-print{background:#6c757d;margin-left:8px;}
.btn-print:hover{background:#555;}
.btn-sm{padding:7px 14px;font-size:14px;}

/* MENSAJES */
.msg-ok{background:#d4edda;color:#155724;padding:12px 20px;border-radius:8px;margin-bottom:15px;font-size:16px;}
.msg-err{background:#f8d7da;color:#721c24;padding:12px 20px;border-radius:8px;margin-bottom:15px;font-size:16px;}

/* LOGIN / REGISTRO */
.login-box{width:460px;margin:60px auto;background:white;padding:40px;border-radius:20px;box-shadow:0 5px 20px rgba(0,0,0,.1);}
.login-box h2{margin-bottom:20px;text-align:center;color:#2d6a4f;}
.login-box input,
.login-box select{width:100%;padding:13px;margin:8px 0;font-size:16px;border:1px solid #ccc;border-radius:8px;}
.tipo-campos{display:none;}
.tipo-campos.visible{display:block;}

/* DASHBOARD ADMIN */
.dashboard{padding:40px;}
.dashboard h1{font-size:52px;margin-bottom:20px;color:#2d6a4f;}

/* NAV ADMIN */
.admin-nav{display:flex;flex-wrap:wrap;gap:12px;margin-bottom:40px;}
.admin-nav a{background:white;border:2px solid #2d6a4f;color:#2d6a4f;padding:12px 22px;border-radius:12px;text-decoration:none;font-weight:bold;font-size:16px;transition:.3s;}
.admin-nav a:hover,.admin-nav a.activo{background:#2d6a4f;color:white;}

/* ADMIN SECTION */
.admin-section{background:white;padding:30px;border-radius:20px;box-shadow:0 5px 15px rgba(0,0,0,.08);margin-bottom:40px;}
.titulo-seccion{font-size:38px;margin-bottom:20px;color:#2d6a4f;}
.acciones-top{display:flex;flex-wrap:wrap;gap:10px;align-items:center;margin-bottom:20px;}

/* CARDS REPORTES */
.cards-reporte{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:20px;margin:20px 0;}
.card-r{background:white;padding:30px;text-align:center;border-radius:16px;box-shadow:0 4px 12px rgba(0,0,0,.1);font-weight:bold;}
.card-r span{font-size:42px;color:#2d6a4f;display:block;}
.card-r small{font-size:16px;color:#555;}

/* FORM INLINE */
.form-inline{display:flex;flex-wrap:wrap;gap:10px;align-items:center;margin-bottom:20px;}
.form-inline input,.form-inline select{padding:10px;font-size:15px;border:1px solid #ccc;border-radius:8px;flex:1;min-width:150px;}

/* FORMULARIO AGREGAR */
.form-agregar{background:#f9f9f9;padding:20px;border-radius:12px;margin-bottom:20px;}
.form-agregar input,.form-agregar select{width:100%;padding:12px;margin:8px 0;font-size:16px;border:1px solid #ccc;border-radius:8px;}

/* TABLA */
table{width:100%;border-collapse:collapse;margin-top:15px;}
table th,table td{border:1px solid #ddd;padding:12px;text-align:center;font-size:16px;}
table th{background:#2d6a4f;color:white;}
table tr:nth-child(even){background:#f9f9f9;}

/* MODAL EDITAR */
.modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:3000;justify-content:center;align-items:center;}
.modal.show{display:flex;}
.modal-box{background:white;padding:30px;border-radius:16px;width:90%;max-width:500px;}
.modal-box h3{margin-bottom:15px;color:#2d6a4f;}
.modal-box input{width:100%;padding:11px;margin:7px 0;font-size:15px;border:1px solid #ccc;border-radius:8px;}

/* MI CUENTA */
.micuenta{padding:40px;max-width:900px;margin:auto;}
.micuenta h1{font-size:40px;color:#2d6a4f;margin-bottom:20px;}
.info-card{background:white;border-radius:16px;padding:25px;box-shadow:0 4px 12px rgba(0,0,0,.08);margin-bottom:25px;}
.info-card h3{color:#2d6a4f;margin-bottom:10px;}
.info-card p{font-size:17px;margin:6px 0;}

/* REPORTE CORREO */
.reporte-correo-form{background:#f9f9f9;padding:20px;border-radius:12px;margin-top:15px;}
.reporte-correo-form input,.reporte-correo-form select{width:100%;padding:11px;margin:7px 0;font-size:15px;border:1px solid #ccc;border-radius:8px;}

/* PRINT */
@media print{
  .no-print{display:none!important;}
  header,.admin-nav,footer{display:none!important;}
  .admin-section{box-shadow:none!important;border:1px solid #ddd!important;}
  .btn-rojo,.btn-print,.acciones-top{display:none!important;}
}

/* RESPONSIVE */
@media(max-width:768px){
  header{flex-direction:column;gap:15px;}
  nav{display:flex;flex-wrap:wrap;justify-content:center;}
  .dashboard h1{font-size:34px;}
  .login-box{width:95%;}
  .micuenta{padding:20px;}
}
</style>
</head>
<body>

<!-- HEADER -->
<header class="no-print">
  <div class="logo">
    <img src="logo.png" alt="Logo">
    <h2>Comedor Comunitario</h2>
  </div>
  <nav>
    <a href="index.php">INICIO</a>
    <a href="index.php?quejas">QUEJAS Y SUGERENCIAS</a>

    <?php if(isset($_SESSION['usuario'])): ?>
      <div class="dropdown">
        <button class="dropdown-btn">👤 <?= htmlspecialchars($_SESSION['usuario']['nombre']) ?> ▾</button>
        <div class="dropdown-content">
          <a href="index.php?micuenta">Mi Cuenta (<?= ucfirst($_SESSION['usuario']['tipo']) ?>)</a>
          <a href="index.php?logout">Cerrar Sesión</a>
        </div>
      </div>
    <?php elseif(isset($_SESSION['admin'])): ?>
      <a href="index.php?admin&seccion=dashboard">PANEL ADMIN</a>
      <a href="index.php?logout">SALIR</a>
    <?php else: ?>
      <div class="dropdown">
        <button class="dropdown-btn">INICIAR SESIÓN ▾</button>
        <div class="dropdown-content">
          <a href="index.php?login&tipo=beneficiario">Beneficiario</a>
          <a href="index.php?login&tipo=voluntario">Voluntario</a>
          <a href="index.php?login&tipo=donante">Donante</a>
          <a href="index.php?login&admin=1">Administrador</a>
        </div>
      </div>
      <a href="index.php?registrarse" class="btn" style="font-size:15px;padding:9px 18px;">REGISTRARSE</a>
    <?php endif; ?>
  </nav>
</header>

<?php

/* ===================== QUEJAS ===================== */
if(isset($_GET['quejas'])){ ?>

<div class="login-box" style="max-width:600px;">
  <h2>📋 Quejas y Sugerencias</h2>
  <?php if(isset($queja_ok)) echo "<div class='msg-ok'>$queja_ok</div>"; ?>
  <form method="POST" class="quejas-form">
    <input type="text" name="nombre" placeholder="Tu nombre" required>
    <input type="email" name="email" placeholder="Tu correo (para responderte)">
    <select name="tipo" required>
      <option value="">-- Tipo --</option>
      <option value="queja">Queja</option>
      <option value="sugerencia">Sugerencia</option>
    </select>
    <textarea name="mensaje" placeholder="Escribe tu mensaje aquí..." required></textarea>
    <button class="btn btn-verde" name="enviar_queja" style="width:100%;">Enviar Mensaje</button>
  </form>
  <br>
  <a class="btn btn-print" href="index.php">← Volver al Inicio</a>
</div>

<?php
/* ===================== REGISTRO USUARIO ===================== */
} elseif(isset($_GET['registrarse'])){ ?>

<div class="login-box" style="max-width:520px;">
  <h2>📝 Crear Cuenta</h2>
  <?php if(isset($error_registro)) echo "<div class='msg-err'>$error_registro</div>"; ?>
  <?php if(isset($registro_ok)) echo "<div class='msg-ok'>$registro_ok <a href='index.php?login'>Iniciar Sesión</a></div>"; ?>

  <form method="POST">
    <input type="text" name="nombre" placeholder="Nombre completo" required>
    <input type="email" name="email" placeholder="Correo electrónico" required>
    <input type="password" name="password" placeholder="Contraseña" required>
    <select name="tipo" id="tipo_registro" required onchange="mostrarCampos(this.value)">
      <option value="">-- ¿Qué tipo de cuenta? --</option>
      <option value="beneficiario">Beneficiario</option>
      <option value="voluntario">Voluntario</option>
      <option value="donante">Donante</option>
    </select>
    <input type="text" name="telefono" placeholder="Teléfono">

    <div class="tipo-campos" id="campos_beneficiario">
      <input type="text" name="direccion" placeholder="Dirección">
    </div>
    <div class="tipo-campos" id="campos_voluntario">
      <input type="text" name="dias" placeholder="Días disponibles (ej: Lunes, Miércoles)">
    </div>
    <div class="tipo-campos" id="campos_donante">
      <input type="text" name="monto_donacion" placeholder="Monto de donación (si aplica)">
    </div>

    <button class="btn btn-verde" name="registrar_usuario" style="width:100%;margin-top:12px;">Crear Cuenta</button>
  </form>
  <p style="text-align:center;margin-top:15px;font-size:16px;">¿Ya tienes cuenta? <a href="index.php?login" style="color:#2d6a4f;font-weight:bold;">Inicia sesión aquí</a></p>
</div>

<script>
function mostrarCampos(tipo){
  document.querySelectorAll('.tipo-campos').forEach(el => el.classList.remove('visible'));
  if(tipo) document.getElementById('campos_'+tipo)?.classList.add('visible');
}
</script>

<?php
/* ===================== LOGIN USUARIO/ADMIN ===================== */
} elseif(isset($_GET['login'])){ 
  $es_admin = isset($_GET['admin']);
?>

<div class="login-box">
  <h2><?= $es_admin ? '🔐 Administrador' : '👤 Iniciar Sesión' ?></h2>
  <?php if(isset($error_login)) echo "<div class='msg-err'>$error_login</div>"; ?>
  <?php if(isset($error_login_u)) echo "<div class='msg-err'>$error_login_u</div>"; ?>

  <?php if($es_admin): ?>
    <form method="POST">
      <input type="text" name="usuario" placeholder="Usuario" required>
      <input type="password" name="password" placeholder="Contraseña" required>
      <button class="btn btn-verde" name="login" style="width:100%;">Entrar como Admin</button>
    </form>
  <?php else: ?>
    <form method="POST">
      <input type="email" name="email" placeholder="Correo electrónico" required>
      <input type="password" name="password" placeholder="Contraseña" required>
      <button class="btn btn-verde" name="login_usuario" style="width:100%;">Iniciar Sesión</button>
    </form>
    <p style="text-align:center;margin-top:15px;font-size:16px;">¿No tienes cuenta? <a href="index.php?registrarse" style="color:#2d6a4f;font-weight:bold;">Regístrate aquí</a></p>
  <?php endif; ?>

  <div style="text-align:center;margin-top:15px;">
    <a href="index.php" style="color:#888;font-size:15px;">← Volver al inicio</a>
  </div>
</div>

<?php
/* ===================== MI CUENTA (USUARIO) ===================== */
} elseif(isset($_GET['micuenta']) && isset($_SESSION['usuario'])){ 
  $u = $_SESSION['usuario'];
?>

<div class="micuenta">
  <h1>Mi Cuenta</h1>
  <div class="info-card">
    <h3>👤 Información Personal</h3>
    <p><b>Nombre:</b> <?= htmlspecialchars($u['nombre']) ?></p>
    <p><b>Correo:</b> <?= htmlspecialchars($u['email']) ?></p>
    <p><b>Tipo de cuenta:</b> <?= ucfirst($u['tipo']) ?></p>
    <p><b>Teléfono:</b> <?= htmlspecialchars($u['telefono']) ?></p>
    <?php if($u['tipo']=='beneficiario'): ?>
      <p><b>Dirección:</b> <?= htmlspecialchars($u['direccion']) ?></p>
    <?php elseif($u['tipo']=='voluntario'): ?>
      <p><b>Días disponibles:</b> <?= htmlspecialchars($u['dias']) ?></p>
    <?php elseif($u['tipo']=='donante'): ?>
      <p><b>Donación registrada:</b> <?= htmlspecialchars($u['monto_donacion']) ?></p>
    <?php endif; ?>
    <p><b>Registro:</b> <?= htmlspecialchars($u['fecha_registro']) ?></p>
  </div>

  <div class="info-card">
    <h3>📊 Mis Reportes</h3>
    <p style="margin-bottom:15px;font-size:16px;">Descarga o envía por correo tus datos registrados.</p>

    <?php if(isset($reporte_correo_ok)) echo "<div class='msg-ok'>$reporte_correo_ok</div>"; ?>

    <div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:15px;">
      <?php
        $tablaUsuario = ($u['tipo']=='beneficiario') ? 'beneficiarios' : (($u['tipo']=='voluntario') ? 'voluntarios' : 'donaciones');
      ?>
      <a class="btn btn-verde" href="index.php?exportar_pdf&tabla=<?= $tablaUsuario ?>" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="index.php?exportar_excel&tabla=<?= $tablaUsuario ?>">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir Página</button>
    </div>

    <div class="reporte-correo-form">
      <b>📧 Enviar reporte por correo:</b>
      <form method="POST">
        <input type="hidden" name="tabla_reporte" value="<?= $tablaUsuario ?>">
        <input type="email" name="correo_destino" placeholder="Correo destino" required value="<?= htmlspecialchars($u['email']) ?>">
        <button class="btn btn-verde" name="enviar_reporte_correo">Enviar Reporte</button>
      </form>
    </div>
  </div>

  <a class="btn btn-rojo" href="index.php?logout">Cerrar Sesión</a>
  <a class="btn btn-print" href="index.php">← Inicio</a>
</div>

<?php
/* ===================== PANEL ADMIN ===================== */
} elseif(isset($_GET['admin']) && isset($_SESSION['admin'])){ ?>

<div class="dashboard">
  <h1>⚙️ Panel Administrador</h1>

  <!-- NAV ADMIN -->
  <nav class="admin-nav no-print">
    <a href="?admin&seccion=dashboard" class="<?= $seccion_admin=='dashboard'?'activo':'' ?>">🏠 Dashboard</a>
    <a href="?admin&seccion=beneficiarios" class="<?= $seccion_admin=='beneficiarios'?'activo':'' ?>">👨‍👩‍👧 Beneficiarios</a>
    <a href="?admin&seccion=voluntarios" class="<?= $seccion_admin=='voluntarios'?'activo':'' ?>">🙋 Voluntarios</a>
    <a href="?admin&seccion=donaciones" class="<?= $seccion_admin=='donaciones'?'activo':'' ?>">💰 Donaciones</a>
    <a href="?admin&seccion=alimentos" class="<?= $seccion_admin=='alimentos'?'activo':'' ?>">🍽️ Alimentos</a>
    <a href="?admin&seccion=usuarios" class="<?= $seccion_admin=='usuarios'?'activo':'' ?>">👥 Usuarios</a>
    <a href="?admin&seccion=quejas" class="<?= $seccion_admin=='quejas'?'activo':'' ?>">📋 Quejas</a>
    <a href="?admin&seccion=reportes" class="<?= $seccion_admin=='reportes'?'activo':'' ?>">📊 Reportes</a>
    <a href="index.php">🌐 Ver Sitio</a>
    <a href="?logout" style="border-color:#e74c3c;color:#e74c3c;">🚪 Salir</a>
  </nav>

  <?php if(isset($reporte_correo_ok)) echo "<div class='msg-ok'>$reporte_correo_ok</div>"; ?>

  <!-- ============ DASHBOARD ============ -->
  <?php if($seccion_admin == 'dashboard'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">🏠 Resumen General</h2>
    <div class="cards-reporte">
      <?php
      $tablas_res = [
        'beneficiarios'=>'👨‍👩‍👧 Beneficiarios',
        'voluntarios'=>'🙋 Voluntarios',
        'donaciones'=>'💰 Donaciones',
        'alimentos'=>'🍽️ Alimentos',
        'usuarios'=>'👥 Usuarios Web',
        'quejas_sugerencias'=>'📋 Quejas/Sugerencias'
      ];
      foreach($tablas_res as $t => $label){
        $cnt = $conn->query("SELECT COUNT(*) as c FROM $t")->fetch_assoc()['c'];
        echo "<div class='card-r'><span>$cnt</span><small>$label</small></div>";
      }
      ?>
    </div>
    <div class="acciones-top">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=beneficiarios" target="_blank">📄 PDF Beneficiarios</a>
      <a class="btn btn-verde" href="?exportar_pdf&tabla=voluntarios" target="_blank">📄 PDF Voluntarios</a>
      <a class="btn btn-verde" href="?exportar_pdf&tabla=donaciones" target="_blank">📄 PDF Donaciones</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir Dashboard</button>
    </div>
  </div>

  <!-- ============ BENEFICIARIOS ============ -->
  <?php elseif($seccion_admin == 'beneficiarios'): ?>
  <div class="admin-section" id="print-area">
    <h2 class="titulo-seccion">👨‍👩‍👧 Beneficiarios</h2>
    <div class="acciones-top no-print">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=beneficiarios" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="?exportar_excel&tabla=beneficiarios">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir</button>
    </div>

    <div class="form-agregar no-print">
      <b style="font-size:18px;">➕ Agregar Beneficiario</b>
      <form method="POST">
        <input type="text" name="nombre" placeholder="Nombre completo" required>
        <input type="text" name="telefono" placeholder="Teléfono" required>
        <input type="text" name="direccion" placeholder="Dirección" required>
        <button class="btn btn-verde" name="guardar_beneficiario">Guardar</button>
      </form>
    </div>

    <table>
      <tr><th>ID</th><th>Nombre</th><th>Teléfono</th><th>Dirección</th><th class="no-print">Acciones</th></tr>
      <?php
      $b = $conn->query("SELECT * FROM beneficiarios ORDER BY id DESC");
      while($r = $b->fetch_assoc()){ ?>
      <tr>
        <td><?= $r['id'] ?></td>
        <td><?= htmlspecialchars($r['nombre']) ?></td>
        <td><?= htmlspecialchars($r['telefono']) ?></td>
        <td><?= htmlspecialchars($r['direccion']) ?></td>
        <td class="no-print">
          <button class="btn btn-verde btn-sm"
            onclick="abrirEditar(<?= $r['id'] ?>,'beneficiarios',
              ['nombre','telefono','direccion'],
              ['<?= addslashes($r['nombre']) ?>','<?= addslashes($r['telefono']) ?>','<?= addslashes($r['direccion']) ?>'])">
            ✏️ Editar
          </button>
          <a class="btn btn-rojo btn-sm" href="?eliminar&id=<?= $r['id'] ?>&tabla=beneficiarios&seccion=beneficiarios"
            onclick="return confirm('¿Eliminar este registro?')">🗑️ Eliminar</a>
        </td>
      </tr>
      <?php } ?>
    </table>
  </div>

  <!-- ============ VOLUNTARIOS ============ -->
  <?php elseif($seccion_admin == 'voluntarios'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">🙋 Voluntarios</h2>
    <div class="acciones-top no-print">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=voluntarios" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="?exportar_excel&tabla=voluntarios">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir</button>
    </div>
    <div class="form-agregar no-print">
      <b style="font-size:18px;">➕ Agregar Voluntario</b>
      <form method="POST">
        <input type="text" name="nombre" placeholder="Nombre" required>
        <input type="text" name="telefono" placeholder="Teléfono" required>
        <input type="text" name="dias" placeholder="Días disponibles" required>
        <button class="btn btn-verde" name="guardar_voluntario">Guardar</button>
      </form>
    </div>
    <table>
      <tr><th>ID</th><th>Nombre</th><th>Teléfono</th><th>Días</th><th class="no-print">Acciones</th></tr>
      <?php $v = $conn->query("SELECT * FROM voluntarios ORDER BY id DESC");
      while($r = $v->fetch_assoc()){ ?>
      <tr>
        <td><?= $r['id'] ?></td>
        <td><?= htmlspecialchars($r['nombre']) ?></td>
        <td><?= htmlspecialchars($r['telefono']) ?></td>
        <td><?= htmlspecialchars($r['dias']) ?></td>
        <td class="no-print">
          <button class="btn btn-verde btn-sm"
            onclick="abrirEditar(<?= $r['id'] ?>,'voluntarios',
              ['nombre','telefono','dias'],
              ['<?= addslashes($r['nombre']) ?>','<?= addslashes($r['telefono']) ?>','<?= addslashes($r['dias']) ?>'])">
            ✏️ Editar
          </button>
          <a class="btn btn-rojo btn-sm" href="?eliminar&id=<?= $r['id'] ?>&tabla=voluntarios&seccion=voluntarios"
            onclick="return confirm('¿Eliminar?')">🗑️ Eliminar</a>
        </td>
      </tr>
      <?php } ?>
    </table>
  </div>

  <!-- ============ DONACIONES ============ -->
  <?php elseif($seccion_admin == 'donaciones'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">💰 Donaciones</h2>
    <div class="acciones-top no-print">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=donaciones" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="?exportar_excel&tabla=donaciones">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir</button>
    </div>
    <div class="form-agregar no-print">
      <b style="font-size:18px;">➕ Agregar Donación</b>
      <form method="POST">
        <input type="text" name="donante" placeholder="Nombre del donante" required>
        <input type="text" name="tipo" placeholder="Tipo (efectivo, especie, etc.)" required>
        <input type="text" name="monto" placeholder="Monto o descripción" required>
        <button class="btn btn-verde" name="guardar_donacion">Guardar</button>
      </form>
    </div>
    <table>
      <tr><th>ID</th><th>Donante</th><th>Tipo</th><th>Monto</th><th class="no-print">Acciones</th></tr>
      <?php $d = $conn->query("SELECT * FROM donaciones ORDER BY id DESC");
      while($r = $d->fetch_assoc()){ ?>
      <tr>
        <td><?= $r['id'] ?></td>
        <td><?= htmlspecialchars($r['donante']) ?></td>
        <td><?= htmlspecialchars($r['tipo']) ?></td>
        <td><?= htmlspecialchars($r['monto']) ?></td>
        <td class="no-print">
          <button class="btn btn-verde btn-sm"
            onclick="abrirEditar(<?= $r['id'] ?>,'donaciones',
              ['donante','tipo','monto'],
              ['<?= addslashes($r['donante']) ?>','<?= addslashes($r['tipo']) ?>','<?= addslashes($r['monto']) ?>'])">
            ✏️ Editar
          </button>
          <a class="btn btn-rojo btn-sm" href="?eliminar&id=<?= $r['id'] ?>&tabla=donaciones&seccion=donaciones"
            onclick="return confirm('¿Eliminar?')">🗑️ Eliminar</a>
        </td>
      </tr>
      <?php } ?>
    </table>
  </div>

  <!-- ============ ALIMENTOS ============ -->
  <?php elseif($seccion_admin == 'alimentos'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">🍽️ Alimentos</h2>
    <div class="acciones-top no-print">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=alimentos" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="?exportar_excel&tabla=alimentos">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir</button>
    </div>
    <div class="form-agregar no-print">
      <b style="font-size:18px;">➕ Agregar Alimento</b>
      <form method="POST">
        <input type="text" name="nombre" placeholder="Nombre del alimento" required>
        <input type="text" name="dia" placeholder="Día de distribución" required>
        <input type="text" name="cantidad" placeholder="Cantidad" required>
        <button class="btn btn-verde" name="guardar_alimento">Guardar</button>
      </form>
    </div>
    <table>
      <tr><th>ID</th><th>Nombre</th><th>Día</th><th>Cantidad</th><th class="no-print">Acciones</th></tr>
      <?php $a = $conn->query("SELECT * FROM alimentos ORDER BY id DESC");
      while($r = $a->fetch_assoc()){ ?>
      <tr>
        <td><?= $r['id'] ?></td>
        <td><?= htmlspecialchars($r['nombre']) ?></td>
        <td><?= htmlspecialchars($r['dia']) ?></td>
        <td><?= htmlspecialchars($r['cantidad']) ?></td>
        <td class="no-print">
          <button class="btn btn-verde btn-sm"
            onclick="abrirEditar(<?= $r['id'] ?>,'alimentos',
              ['nombre','dia','cantidad'],
              ['<?= addslashes($r['nombre']) ?>','<?= addslashes($r['dia']) ?>','<?= addslashes($r['cantidad']) ?>'])">
            ✏️ Editar
          </button>
          <a class="btn btn-rojo btn-sm" href="?eliminar&id=<?= $r['id'] ?>&tabla=alimentos&seccion=alimentos"
            onclick="return confirm('¿Eliminar?')">🗑️ Eliminar</a>
        </td>
      </tr>
      <?php } ?>
    </table>
  </div>

  <!-- ============ USUARIOS WEB ============ -->
  <?php elseif($seccion_admin == 'usuarios'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">👥 Usuarios Registrados</h2>
    <div class="acciones-top no-print">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=usuarios" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="?exportar_excel&tabla=usuarios">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir</button>
    </div>
    <table>
      <tr><th>ID</th><th>Nombre</th><th>Email</th><th>Tipo</th><th>Teléfono</th><th class="no-print">Eliminar</th></tr>
      <?php $us = $conn->query("SELECT * FROM usuarios ORDER BY id DESC");
      while($r = $us->fetch_assoc()){ ?>
      <tr>
        <td><?= $r['id'] ?></td>
        <td><?= htmlspecialchars($r['nombre']) ?></td>
        <td><?= htmlspecialchars($r['email']) ?></td>
        <td><?= ucfirst($r['tipo']) ?></td>
        <td><?= htmlspecialchars($r['telefono']) ?></td>
        <td class="no-print">
          <a class="btn btn-rojo btn-sm" href="?eliminar&id=<?= $r['id'] ?>&tabla=usuarios&seccion=usuarios"
            onclick="return confirm('¿Eliminar usuario?')">🗑️</a>
        </td>
      </tr>
      <?php } ?>
    </table>
  </div>

  <!-- ============ QUEJAS ADMIN ============ -->
  <?php elseif($seccion_admin == 'quejas'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">📋 Quejas y Sugerencias</h2>
    <div class="acciones-top no-print">
      <a class="btn btn-verde" href="?exportar_pdf&tabla=quejas_sugerencias" target="_blank">📄 Exportar PDF</a>
      <a class="btn" href="?exportar_excel&tabla=quejas_sugerencias">📊 Exportar Excel</a>
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir</button>
    </div>
    <table>
      <tr><th>ID</th><th>Nombre</th><th>Email</th><th>Tipo</th><th>Mensaje</th><th>Fecha</th><th class="no-print">Eliminar</th></tr>
      <?php $q = $conn->query("SELECT * FROM quejas_sugerencias ORDER BY id DESC");
      while($r = $q->fetch_assoc()){ ?>
      <tr>
        <td><?= $r['id'] ?></td>
        <td><?= htmlspecialchars($r['nombre']) ?></td>
        <td><?= htmlspecialchars($r['email']) ?></td>
        <td><?= ucfirst($r['tipo']) ?></td>
        <td><?= htmlspecialchars($r['mensaje']) ?></td>
        <td><?= htmlspecialchars($r['fecha']) ?></td>
        <td class="no-print">
          <a class="btn btn-rojo btn-sm" href="?eliminar&id=<?= $r['id'] ?>&tabla=quejas_sugerencias&seccion=quejas"
            onclick="return confirm('¿Eliminar?')">🗑️</a>
        </td>
      </tr>
      <?php } ?>
    </table>
  </div>

  <!-- ============ REPORTES ============ -->
  <?php elseif($seccion_admin == 'reportes'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">📊 Exportar Reportes</h2>
    <p style="font-size:17px;margin-bottom:20px;">Descarga reportes en PDF o Excel de cada módulo del sistema.</p>

    <?php
    $modulos = [
      'beneficiarios' => '👨‍👩‍👧 Beneficiarios',
      'voluntarios'   => '🙋 Voluntarios',
      'donaciones'    => '💰 Donaciones',
      'alimentos'     => '🍽️ Alimentos',
      'usuarios'      => '👥 Usuarios Web',
      'quejas_sugerencias' => '📋 Quejas/Sugerencias'
    ];
    foreach($modulos as $tabla => $nombre){
      $cnt = $conn->query("SELECT COUNT(*) as c FROM $tabla")->fetch_assoc()['c'];
      echo "
      <div style='background:#f9f9f9;border-radius:12px;padding:15px 20px;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;'>
        <div>
          <b style='font-size:18px;'>$nombre</b>
          <span style='color:#888;margin-left:10px;font-size:15px;'>($cnt registros)</span>
        </div>
        <div style='display:flex;gap:8px;'>
          <a class='btn btn-verde btn-sm' href='?exportar_pdf&tabla=$tabla' target='_blank'>📄 PDF</a>
          <a class='btn btn-sm' href='?exportar_excel&tabla=$tabla'>📊 Excel</a>
        </div>
      </div>";
    }
    ?>
    <div style="margin-top:20px;">
      <button onclick="window.print()" class="btn btn-print">🖨️ Imprimir esta página</button>
    </div>
  </div>

  <!-- ============ MÓDULO CORREOS ============ -->
  <?php elseif($seccion_admin == 'correos'): ?>
  <div class="admin-section">
    <h2 class="titulo-seccion">📧 Envío de Correos</h2>
    <p style="font-size:17px;margin-bottom:20px;">Envía reportes por correo electrónico a cualquier destinatario.</p>

    <?php if(isset($reporte_correo_ok)) echo "<div class='msg-ok' style='margin-bottom:20px;'>$reporte_correo_ok</div>"; ?>

    <div class="reporte-correo-form" style="max-width:500px;">
      <form method="POST">
        <label style="font-size:16px;font-weight:bold;">Módulo a reportar:</label>
        <select name="tabla_reporte" required>
          <option value="">-- Seleccionar módulo --</option>
          <option value="beneficiarios">Beneficiarios</option>
          <option value="voluntarios">Voluntarios</option>
          <option value="donaciones">Donaciones</option>
          <option value="alimentos">Alimentos</option>
          <option value="usuarios">Usuarios Web</option>
          <option value="quejas_sugerencias">Quejas y Sugerencias</option>
        </select>
        <label style="font-size:16px;font-weight:bold;margin-top:10px;display:block;">Correo destinatario:</label>
        <input type="email" name="correo_destino" placeholder="ejemplo@correo.com" required>
        <button class="btn btn-verde" name="enviar_reporte_correo" style="width:100%;">📤 Enviar Reporte por Correo</button>
      </form>
    </div>

    <div style="margin-top:25px;background:#fff3cd;border-radius:10px;padding:15px 20px;font-size:15px;color:#856404;">
      <b>⚠️ Nota sobre correos:</b><br>
      El módulo de correos usa la función <code>mail()</code> de PHP. En producción (servidor real con dominio), los correos funcionarán correctamente. En entorno local (XAMPP/WAMP) se requiere configurar un servidor SMTP como <b>Mailhog</b>, <b>Mailtrap</b> o <b>PHPMailer con SMTP de Gmail</b> para el envío efectivo.
    </div>

    <button onclick="window.print()" class="btn btn-print" style="margin-top:15px;">🖨️ Imprimir</button>
  </div>
  <?php endif; ?>

</div><!-- /dashboard -->

<?php
/* ===================== PÁGINA PRINCIPAL ===================== */
} else { ?>

<!-- CARRUSEL -->
<div class="carrusel no-print">
  <div class="slide active">
    <img src="imagenes/imagen3.jpg" alt="Cocinando con amor">
    <div class="texto">Cocinando con amor</div>
  </div>
  <div class="slide">
    <img src="imagenes/imagen4.jpg" alt="Un lugar para todos">
    <div class="texto">Un lugar para todos</div>
  </div>
  <div class="slide">
    <img src="imagenes/imagen1.jpg" alt="Una comida puede cambiar un día entero">
    <div class="texto">Una comida puede cambiar un día entero</div>
  </div>
  <div class="slide">
    <img src="https://images.unsplash.com/photo-1488521787991-ed7bbaae773c" alt="Tu ayuda llega lejos">
    <div class="texto">Tu ayuda llega lejos</div>
  </div>
</div>

<!-- INTRO -->
<section class="intro">
  <h1>Bienvenidos</h1>
  <p>
    Nuestro comedor comunitario brinda apoyo alimentario,
    ayuda social y esperanza a muchas familias.
    Gracias a los voluntarios y donaciones podemos seguir ayudando.
  </p>

  <!-- LINKS CUENTA -->
  <div class="inicio-links no-print">
    <a href="index.php?registrarse">📝 Regístrate</a>
    <a href="index.php?login">🔑 Ya tengo una cuenta</a>
    <a href="index.php?quejas">💬 Quejas y Sugerencias</a>
  </div>
</section>

<!-- CONTACTO -->
<section class="contacto" id="contacto">
  <div class="contacto-container">
    <div class="info-contacto">
      <h2>Contacto</h2>
      <p><b>Dirección:</b><br>Calle Principal #123</p>
      <p><b>Horario:</b><br>Lunes a Viernes 8am - 5pm</p>
      <p><b>Teléfono:</b><br>4420000000</p>
      <p><b>Correo:</b><br>comedor@gmail.com</p>
    </div>
	
	<!-- MAPA -->
<div class="mapa" style="flex:1;min-width:300px;">
  <h2 style="color:#2d6a4f;font-size:40px;margin-bottom:20px;">📍 Ubicación</h2>
  <iframe
    src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d60864.23!2d-92.6376!3d16.7569!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85ecd8fb3adb94e9%3A0x2c4376050d9e3f3f!2sTuxtla%20Guti%C3%A9rrez%2C%20Chiapas!5e0!3m2!1ses!2smx!4v1700000000000"
    width="100%"
    height="300"
    style="border:0;border-radius:15px;box-shadow:0 4px 12px rgba(0,0,0,.15);"
    allowfullscreen=""
    loading="lazy"
    referrerpolicy="no-referrer-when-downgrade">
  </iframe>
</div>
	


 
  </div>
</section>

<footer>
  Comedor Comunitario © 2026 
  
</footer>

<?php } ?>

<!-- MODAL EDITAR -->
<div class="modal no-print" id="modalEditar">
  <div class="modal-box">
    <h3>✏️ Editar Registro</h3>
    <form method="POST" id="formEditar">
      <input type="hidden" name="editar_registro" value="1">
      <input type="hidden" name="id" id="edit_id">
      <input type="hidden" name="tabla" id="edit_tabla">
      <div id="edit_campos"></div>
      <div style="display:flex;gap:10px;margin-top:10px;">
        <button class="btn btn-verde" type="submit">💾 Guardar Cambios</button>
        <button class="btn btn-print" type="button" onclick="cerrarModal()">Cancelar</button>
      </div>
    </form>
  </div>
</div>

<script>
// CARRUSEL
let slides = document.querySelectorAll('.slide');
let index = 0;
if(slides.length > 0){
  slides.forEach(s => s.classList.remove('active'));
  slides[0].classList.add('active');
  setInterval(()=>{
    slides[index].classList.remove('active');
    index = (index + 1) % slides.length;
    slides[index].classList.add('active');
  }, 3500);
}

// MODAL EDITAR
function abrirEditar(id, tabla, campos, valores){
  document.getElementById('edit_id').value = id;
  document.getElementById('edit_tabla').value = tabla;
  let html = '';
  campos.forEach((c,i) => {
    html += `<input type="text" name="${c}" placeholder="${c.charAt(0).toUpperCase()+c.slice(1)}" value="${valores[i]}" required>`;
  });
  document.getElementById('edit_campos').innerHTML = html;
  document.getElementById('modalEditar').classList.add('show');
}

function cerrarModal(){
  document.getElementById('modalEditar').classList.remove('show');
}

document.getElementById('modalEditar')?.addEventListener('click', function(e){
  if(e.target === this) cerrarModal();
});
</script>

</body>
</html>