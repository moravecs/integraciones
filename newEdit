<? 
include_once('../configuracion.php');
include('../seguridad.php');
include_once('../functions.php');

$id 				= 	$_REQUEST["id"];

if ($id=='') { header('Location:../src/a/panel.php'); exit;}

$sql 				= 	"SELECT Curso,idcurso,Centro,Fecha,Nombre,Apellidos,FechaNacimiento,Email,Direccion,Piso,Telefono,Puerta,Dni,Edad,Cp,Poblacion,Pais,Nacionalidad,NivelEstudios,SituacionLaboral,Traspaso,Test,Web,Integraciones,Lssi,Robinson,Ip,Empresa,SectorActividad,xpot,ContactId FROM cupones Where Id = ".$id." LIMIT 1";
$rs 				= 	mysql_query($sql,$link); 
		mysql_query ("SET NAMES 'utf8'"); 	   

$fila 				= 	mysql_fetch_object($rs);	   

$curso 				= 	utf8_encode($fila->Curso);
$idcurso 			= 	$fila->idcurso;
$pos				= 	strpos($idcurso, '-');

$centroCupon		=	$fila->Centro;
$nuevoid			=	($pos === false) ? $centroCupon.'-'.$idcurso : $idcurso;
$fecha_cupon		= 	$fila->Fecha;
$nombre 			= 	ucwords(strtolower($fila->Nombre));
$apellidos 			= 	ucwords(strtolower($fila->Apellidos));
$fecha				= 	$fila->FechaNacimiento;
$email 				= 	$fila->Email;
$direccion 			= 	($fila->Direccion);
$piso 				= 	$fila->Piso;
$telefono 			= 	$fila->Telefono;
$puerta 				= 	$fila->Puerta;
$dni 				= 	$fila->Dni;
$edad 				= 	$fila->Edad;
$cp 					= 	$fila->Cp;
// Obtenemos el valor para saber si proviene de una campaña (20140407 campña activa en cursos-trabjadores para masterD SEPE empresas del metal barcelona: EMP20140407-XXX)
$xpot 				= 	$fila->xpot;

//Comprobamos si proviene de una campaña y lo señalamos con una alerta
	if (($xpot) && ($xpot!='')) {
		$campanas	=	'<div class="alert alert-warning">Este cupón Proviene de una <b>campaña </b><span class="float-right">'.$xpot.'</span></p></div>';
	}
echo $campana;

//	Si ya está en el zoho mostramos que se le pueden enviar notas al Contacto:
$contactId			=	$fila->ContactId;

$poblacion 			= 	($fila->Poblacion);
// Si no hay problación, miramos en la BBDD y recuperamos el valor
if ($poblacion 		==	'') {
			$sql_encuentra_provincia 	=	"SELECT nom FROM getpoblacion_cps where cp='".$cp."'";
	//		echo $sql_encuentra_provincia.'<br>';
			$rs_encuentra_provincia 	= 	mysql_query($sql_encuentra_provincia,$link); 


			$fila_encuentra_provincia 	= 	mysql_fetch_object($rs_encuentra_provincia);
			$poblacion_bbdd 			= 	($fila_encuentra_provincia->nom);
//Como la tabla de provincias y CP está codificada en UTF(, primero la descodificamos y después la volvemos a codificar para que quede bien
			$text 	= 	(($poblacion_bbdd));
			
			$sql_update_provincia 		=	"UPDATE cupones SET Poblacion = '".(($text))."' where Id =".$id;
	//			echo($sql_update_provincia);
			$rs_updateprovincia 		= 	mysql_query($sql_update_provincia,$link);
			$poblacion 					= 	$test; 
}

$pais 				= 	$fila->Pais;
$nacionalidad 		= 	$fila->Nacionalidad;
$NivelEstudios 		= 	$fila ->NivelEstudios;
$SituacionLaboral 	= 	$fila ->SituacionLaboral;
$traspaso 			= 	$fila->Traspaso;
$test 				= 	$fila->Test;
$web 				= 	$fila->Web;
$integraciones 		= 	trim($fila->Integraciones);
$integraciones 		= 	explode(",",$integraciones);
$lssi 				= 	$fila ->Lssi;
$robinson 			= 	$fila ->Robinson;
$ip 				= 	$fila->Ip;
if ($pais 			== 	66) {
  $pais_textual 	= 	"España";
}
// Seleccionamos el nombre de la provincia pero guardamos el código en el campo oculto siguiente
$cod_pro 			= 	substr(trim($cp),0,2);
$sql_pro 			= 	"SELECT Nombre,Id FROM provincias where Id = ".$cod_pro;
$rs_pro 			= 	mysql_query($sql_pro,$link); 
//mysql_query("SET CHARACTER SET utf8");
//mysql_query("SET NAMES utf8"); 
$fila_pro 			= 	mysql_fetch_object($rs_pro);
$provincia_nombre 	= 	utf8_decode($fila_pro->Nombre);
$provincia_id 		= 	$fila_pro->Id;

//Si es un lead de empresa, recogemos la información
$empresa 			= 	$fila->Empresa;
$sectoractividad 	= 	$fila->SectorActividad;

//Actualización de la dirección
$patron  			=	"/Medes/";
$tpmaddress 		= 	preg_match($patron, $direccion, $coincidencias,PREG_OFFSET_CAPTURE);
//Miramos que la direcció sea mayore que 4 posiciones y no contenga Medes //
if ((strlen($direccion)>4) && (!($tpmaddress))) {
	
		$direccion	=	sanitizeString(utf8_encode($direccion));
		//echo $coma_al_final.'"<br>';
		$direccion	= 	trim($direccion);
		$partes_direccion = explode(" ", $direccion);

		foreach ($partes_direccion as $parte)
			{ 
			if (is_numeric($parte)) {$numerico = $numerico+1;}
			}
			//echo $numerico.'<br>';

		if (!($numerico)){$direccion = $direccion.', '.rand(1,10);}
		
		$sql_update_direccion ="UPDATE cupones SET Direccion = '".$direccion."' where Id =".$id;
		//echo($sql_update_direccion);
		$rs 		= 	mysql_query($sql_update_direccion,$link); 
//		$direccion = $direccion;
		}

?>
<?
//						Tabla de las integraciones
$sql 						= 	"SELECT Id,Nombre FROM centros WHERE Activo='0' order by nombre asc";
$rs 						= 	mysql_query($sql,$link); 
while ($fila_integracion 	= 	mysql_fetch_object($rs)){
	$idcentroIntegracion	= 	$fila_integracion->Id;
	$nombreIntegracion		=	$fila_integracion->Nombre;
	$fila_numero++ ;
	$tablaIntegraciones		.= '<td><a href="integraciones.php?id='.$idcentroIntegracion.'&idlead='.$id.'&amp;keepThis=true&amp;TB_iframe=true&amp;height=350&amp;width=800" class="thickbox" title="Integración con '.$nombreIntegracion.'"';
	$tablaIntegraciones 	.= 	in_array($idcentroIntegracion,$integraciones)? "style='color:green; font-weight:bolder;'":'';
	$tablaIntegraciones		.=	">".$nombreIntegracion;
	if(count($integraciones) <>0){    
	if (in_array($idcentroIntegracion,$integraciones)){
		$tablaIntegraciones .=	"</a> <a href='desmarcar.php?id=".$id."&amp;idcentro=".$idcentroIntegracion."' class='desmarcar_cupon' style='color:green;' title='Desmarcar Cupon'> <i class='fa fa-check'></i></a></td>";
		}	else 	{
		$tablaIntegraciones .= 	' <i class="fa fa-times" aria-hidden="true" style="color:red;"></i>'; 
		}
		}	else	{
		$tablaIntegraciones .= 	' <i class="fa fa-times" aria-hidden="true" style="color:red;"></i>'; 
		}
		$tablaIntegraciones .= 	'</a></td>';
		if ($fila_numero 	== 	3){$tablaIntegraciones 	.= '</tr><tr>'; $fila_numero = 0; }
; }
// echo $tablaIntegraciones;
?>
<?
//						Selección de dispositivo del cupón
$sql						=	"SELECT Device FROM cuponesExtra WHERE Id = '$id'";
$rs 						= 	mysql_query($sql,$link); 
$filaDevice		 			= 	mysql_fetch_object($rs);
$device						=	$filaDevice->Device;
//$device						=	$filaDevice['Device'];
switch ($device) {
	case 'computer':
		$dispositivo		=	'<hr /><i class="fa fa-desktop fa-2x" aria-hidden="true"></i>  <span class="h4" style="padding-left:20px;">Ordenador</span>';
		break;
	case 'phone':
		$dispositivo		=	'<hr /><i class="fa fa-mobile fa-3x" aria-hidden="true"></i>  <span class="h4" style="padding-left:20px;">Móvil</span>';
		break;
	case 'tablet':
		$dispositivo		=	'<hr /><i class="fa fa-tablet fa-3x" aria-hidden="true"></i>  <span class="h4" style="padding-left:20px;">Tablet</span>';
		break;
	default:
		$dispositivo		=	'';
		break;

}

?>
<!doctype html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<title>CMS - Editar Cupones - Cupon ID <?=$id; ?> </title>
<!--<link href="../inc/css/estilos+.css" rel="stylesheet" type="text/css">
--><link type='text/css' href='../../inc/css/thick.css' rel='stylesheet' media='screen' />
    <!--[if lt IE 9]
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
<link href="http://www.tpm-corp.es/src/a/inc/css/bootstrap.min.last.css" rel="stylesheet">
<!-- Optional theme -->
<link href="http://www.tpm-corp.es/src/a/inc/css/bootstrap-theme.min.css" rel="stylesheet">
<link href="http://www.tpm-corp.es/src/a/inc/css/style.css" rel="stylesheet">
<link href="http://www.tpm-corp.es/src/a/inc/css/bootstrap-toggle.min.css" rel="stylesheet">
<link href="http://www.tpm-corp.es/src/a/inc/css/sweet-alert.css" rel="stylesheet" type="text/css" >
<link href="http://www.tpm-corp.es/src/a/inc/css/bootstrap-milestones.min.css" rel="stylesheet" type="text/css" >
<link href="http://www.tpm-corp.es/src/a/inc/css/pace.css" rel="stylesheet">
	<style>
		@import url(//cdnjs.cloudflare.com/ajax/libs/normalize/3.0.1/normalize.min.css);
		@import url(//maxcdn.bootstrapcdn.com/font-awesome/4.6.0/css/font-awesome.min.css);
	</style>
<link href="//cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.css" rel="stylesheet">

<style>
#TB_window {
position: fixed;
background: #ffffff;
z-index: 102;
color:#000000;
display:none;
border: 4px solid #525252;
text-align:left;
top:20%;
left:50%;
}
#notasCupon, #resultadoEncuesta, #enviarEncuesta, #contenedorEncuesta, #notaNew, #stripjourneypanel {display:none;}
.mb10 {margin-bottom:10px;}
.mb20 {margin-bottom:20px;}
.mb30 {margin-bottom:30px;}
.notaCRM 	{width:100%; border:1px solid #EBEBEB; display:block !important; padding:10px;}
.fechaNota  { width:30%; display:inline; margin-right:20px; }
.noteTitle	{width:60%; display:inline;}
.noteContent { margin-top:10px;}
#tenemosEncuesta {cursor:pointer;}
/*#extraCRM{margin:15px 0 !important; padding-top: 30px!important; height:90px; border:1px solid #EFEFEF;}*/
#igualar	{cursor:pointer;}
.info { background: #dbe3ff; border:1px solid #a2b4ee; color: #585b66; -moz-box-shadow: 0px 0px 4px #333; -webkit-box-shadow: 0px 0px 4px #333; box-shadow: 0px 0px 4px #333;  background-image: url('../img/alerta.png');}

    html, body, #map-canvas {
      margin: 0;
      padding: 0;
      height: 100%;
    }
      body {
        padding-top: 40px; /* 60px to make the container go all the way to the bottom of the topbar */
      }
	  .chart {
	  position: relative;
	  display: inline-block;
	  width: 150px;
	  height: 150px;
	  margin-top: 50px;
	  margin-bottom: 50px;
	  text-align: center;
	  margin-right:22px;
	  font-weight:bold;
	}
	.chart canvas {
	  position: absolute;
	  top: 0;
	  left: 0;
	}
	.percent {
	  display: inline-block;
	  line-height: 160px;
	  z-index: 2;
	}
	.percent:after {
	  content: '%';
	  margin-left: 0.1em;
	  font-size: .8em;
	}
	#statsChart {
	  width: 97%;
	  height: 250px;
	  margin: 65px auto;
	   }
#cuponesxweb .badge {
    position:relative;
    right:10px;
    top:-10px;
    z-index:100;
}
.archivosRecibidos .badge, .matriculas .badge ,.mensajesPendientes .badge, .leadstats .badge{
    position:relative;
    right:20px;
    top:-20px;
    z-index:100;
	font-size: 12px;
}
.badge.bg-success {
    background:#a9d86e;
}
.badge.bg-warning {
    background:#FCB322;
}
.badge.bg-important {
    background:#ff6c60;
}
.badge.bg-info {
    background:#41cac0;
}
#cuponesxweb .fa-envelope-o{
	font-size:160%;
	}
.detalles { cursor:pointer;}

.timeline.label-info {font-size:20px;}

label {padding-right:20px;}

#leadData {font-size:16px;}
.spacedown { padding-bottom:15px;}
.spacedown i {padding-right:10px;}

.leadstats i {font-size:36px;}
.datastat {margin-bottom: 5%}
.datastat i {padding-left:30%;}


/*! bootstrap3-wysihtml5-bower 2014-06-11 */

ul.wysihtml5-toolbar{margin:0;padding:0;display:block}ul.wysihtml5-toolbar::after{clear:both;display:table;content:""}ul.wysihtml5-toolbar>li{float:left;display:list-item;list-style:none;margin:0 5px 10px 0}ul.wysihtml5-toolbar a[data-wysihtml5-command=bold]{font-weight:700}ul.wysihtml5-toolbar a[data-wysihtml5-command=italic]{font-style:italic}ul.wysihtml5-toolbar a[data-wysihtml5-command=underline]{text-decoration:underline}ul.wysihtml5-toolbar a.btn.wysihtml5-command-active{background-image:none;-webkit-box-shadow:inset 0 2px 4px rgba(0,0,0,.15),0 1px 2px rgba(0,0,0,.05);-moz-box-shadow:inset 0 2px 4px rgba(0,0,0,.15),0 1px 2px rgba(0,0,0,.05);box-shadow:inset 0 2px 4px rgba(0,0,0,.15),0 1px 2px rgba(0,0,0,.05);background-color:#E6E6E6;background-color:#D9D9D9;outline:0}ul.wysihtml5-commands-disabled .dropdown-menu{display:none!important}ul.wysihtml5-toolbar div.wysihtml5-colors{display:block;width:50px;height:20px;margin-top:2px;margin-left:5px;position:absolute;pointer-events:none}ul.wysihtml5-toolbar a.wysihtml5-colors-title{padding-left:70px}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=black]{background:#000!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=silver]{background:silver!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=gray]{background:gray!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=maroon]{background:maroon!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=red]{background:red!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=purple]{background:purple!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=green]{background:green!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=olive]{background:olive!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=navy]{background:navy!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=blue]{background:#00f!important}ul.wysihtml5-toolbar div[data-wysihtml5-command-value=orange]{background:orange!important}.glyphicon-quote:before{content:"\201C";font-family:Georgia,serif;font-size:50px;position:absolute;top:-4px;left:-3px;max-height:100%}.glyphicon-quote:after{content:"\0000a0"}

.oculto {visibility:hidden;}
@media print {
.navbar, .panel-heading, .noimpress { display: none !important;}
#notes, #documents, #messages,#edad{ display: none !important; width:0px, height:0px;}
div {display:inline-block;}
.printable { visibility:visible;}
.col-md-12 { width:100%;}



}

.btn-file {
    position: relative;
    overflow: hidden;
}
.btn-file input[type=file] {
    position: absolute;
    top: 0;
    right: 0;
    min-width: 100%;
    min-height: 100%;
    font-size: 100px;
    text-align: right;
    filter: alpha(opacity=0);
    opacity: 0;
    outline: none;
    background: white;
    cursor: inherit;
    display: block;
}
input[readonly] {
  background-color: white !important;
  cursor: text !important;
}
.panel-footer.panel-custom {
    background: white;
    color: black;
}
.panel-footer.footer-custom {
    background: #5cb85c;
    color: white;
}
#verIntegraciones 	{ cursor:pointer;}
.panel-refresh {
 height:250px;
 position:relative;
}
#messageszoho{ height:350px; text-align:center; display:block; margin:40px 0; color:#d3d3d3 !important;} 
.refresh-container {
 position:absolute;
 top:0;
 right:0;
 background:rgba(200,200,200,0.25);
 width:100%;
 height:100%;
 display: none;
 text-align:center;
 z-index:4;
}
.refresh-spinner {
 padding: 30px;
 opacity: 0.8;
}
.btn-is-disabled {
  pointer-events: none; /* Disables the button completely. Better than just cursor: default; */
  opacity:0.7;
  @include opacity(0.1);
}
.noresize {
  resize: none; 
}
.send { background-color:green;}
</style>

</head>
<body>
<? include ('../src/a/inc/inc_navegacion.php'); ?>    
    <div class="container">
       <div class="row page-header" >
         <div class="row">
                <div class="col-lg-3 col-md-3 col-sm-6">
                    <div class="panel panel-info">
                        <div class="panel-body" >
                            <p style="font-size:18px; font-weight:bolder;" ><span id="Nombre"><?=ucwords(utf8_encode($nombre));?></span> <span id="Apellidos"><?=ucwords(utf8_encode($apellidos));?></span></p>
                            <p><b><span id="Edad"><?=$edad;?></span> años</b> <?=es_menor($edad); ?></p>
                            <p ><span id="Email"><?=$email;?></span> <a href='maps_duplicadas.php?id=<?=$id?>&amp;repetido=email&amp;keepThis=true&amp;TB_iframe=true&amp;height=300&amp;width=780' class='thickbox' target='_blank' title='Comprobar duplicados'><?=revisar_email($email);?></a></p> 
                            <p> <span id="Telefono"><?=$telefono;?></span> <a href='maps_duplicadas.php?id=<?=$id?>&amp;repetido=telefono&amp;keepThis=true&amp;TB_iframe=true&amp;height=300&amp;width=780' class='thickbox' target='_blank' title='Comprobar duplicados'><?=revisar_telefono($telefono);?></a></p>
                            <? if (($direccion) || !($direccion ==',')) { ?>
                            <p><span id="Direccion"><?=(ucwords(strtolower($direccion)));?></span> <span id="Piso"><?=(($piso));?></span> <span id="Puerta"><?=($puerta);?></span></p>
                            <? ;} ?>
                            <p><span id="Cp"><?=$cp;?></span> <span id="Poblacion"><?=ucwords(utf8_encode($poblacion));?></span> - <?=utf8_encode($provincia_nombre);?></p>
                            <p><?=$pais_textual; ?></p>
                            <hr />
                            <p id="NivelEstudios"><?=utf8_decode(nivel_estudios($NivelEstudios));?></p>
                            <hr />
                            <p> <span id="SituacionLaboral"><?=situacion_laboral($SituacionLaboral);?></span><?=$igualarSituaciones = revisar_email($email) !=' ' ? '<span id="igualar" > <i class="fa fa-refresh igualarspin" aria-hidden="true" title="Igualar situación laboral"></i></span>' :'';?></p>
			<? if ((($empresa) || ($sectoractividad)) && $centroCupon!='52'){?>
                <?	$sectoractividad = (strlen(sector_actividad($sectoractividad)) > 70) ? substr(sector_actividad($sectoractividad), 0, 65) . "..." : sector_actividad($sectoractividad); ?>         
            <p>Sector: <span id="SectorActividad"><?=utf8_decode($sectoractividad);?></span></p>
            	<? ;} ?>
                <? if ((($empresa) || ($sectoractividad)) && $centroCupon!='52'){?>
                            <p>Empresa: <span id="Empresa"><?=$datosempresa = ($empresa=='') ? 'Curso Subvencionado' : $empresa ;?></span></p> 
                <? ;} ?> 
                       <?=$dispositivo;?>
                        </div>
                    </div>
                    <div class="row mb30 col-md-12" >
                    <button class="btn btn-default" id="verNotasBack"><i class="fa fa-list" aria-hidden="true"></i></button>
                    <button class="btn btn-default" id="marcarTraspasadoTPM"><i class="fa fa-check" aria-hidden="true"></i></button>
                    </div>
                </div>
                <div class="col-lg-6 col-md-3 col-sm-6">
                    <div class="panel <?=$oculto= $test =='1'? 'panel-default': ($traspaso=='1' ? 'panel-success' : 'panel-info');?> <?=$lssirobinson = $lssi == 1? 'panel-danger' :($robinson=='1' ? 'panel-danger' : ($traspaso=='1' ? 'panel-success' : 'panel-info'));?> ">
                        <div class="panel-heading">
                            <h5 >
                            <span id="Curso">
                                <?=$curso	=	(strlen($curso) > 80) ? substr($curso, 0, 75) . "..." : $curso;?>
                                <?=$oculto= $test =='1'? ' (<strong>Oculto</strong>)':'';?>
                            </span>
                            </h5>
                        </div>
                        <div class="panel-body" >
                        	<div class="col-lg-2 col-md-2 col-xs-4">
                            	<p>Marca:</p>
                            </div>
                        	<div class="col-lg-10 col-md-10 col-xs-8">
                            	<p id="Centro"></p>
                            </div>
                        	<div class="col-lg-2 col-md-2 col-xs-4">
                            	<p>Origen:</p>
                            </div>
                        	<div class="col-lg-6 col-md-6 col-xs-8">
                            	<p><?=$web;?></p>
                            </div>
                        	<div class="col-lg-4 col-md-4 col-xs-12">
                            	<p>(<?=f_datef($fecha_cupon);?>)</p>
                            </div>
                        	<div class="col-lg-2 col-md-2 col-xs-3">
                            	<p>Lssi:</p>
                            </div>
                        	<div class="col-lg-1 col-md-1 col-xs-3">
                            	<p ><?=revisar_legales($lssi)== 'NO marcado' ? '<i class="fa fa-check" aria-hidden="true" style="color:green;"></i>' : '<i class="fa fa-close" aria-hidden="true" style="color:red; font-weight:bolder;"></i>';?></p>
                            </div>
                        	<div class="col-lg-2 col-md-2 col-xs-3">
                            	<p>Robinson:</p>
                            </div>
                        	<div class="col-lg-1 col-md-1 col-xs-3">
                            	<p><?=revisar_legales($robinson)== 'NO marcado' ? '<i class="fa fa-check" aria-hidden="true" style="color:green;"></i>' : '<i class="fa fa-close" aria-hidden="true" style="color:red; font-weight:bolder;"></i>';?></p>
                            </div>
                        	<div class="col-lg-1 col-md-1 col-xs-4">
                            	IP:
                            </div>
                        	<div class="col-lg-4 col-md-4 col-xs-8">
								<?=$ip;?> 
								<? $ips = explode (".",$ip); $ip_final= $ips[0].".".$ips[1].".".$ips[2];?>
                                <a href='maps_ip.php?id=<?=$id?>&amp;keepThis=true&amp;TB_iframe=true&amp;height=300&amp;width=780' class='thickbox' target='_blank' title='Comprobar IPs'><?=ip_duplicada($ip_final);?></a>
                            </div>
                            <div class="col-lg-12 col-md-12" >
                        	<div class="col-lg-2 col-md-2 col-xs-4">
                            	<p>Oculto:</p>
                            </div>
                        	<div class="col-lg-10 col-md-10 col-xs-8">
                            	<p id="Test"><?=cupon_oculto($test);?></p>
                            </div>
                            </div>
                        </div>

                        <div class="panel-footer footer-custom <?=$checkTraspaso = $traspaso==1 ? '' : 'hidden';?>">
						Traspasado a <?=quecentro($integraciones[0]);?> <i class="fa fa-check-square-o"></i>
                        <span class="pull-right" id="verIntegraciones"><i class="fa fa-plus-square"></i> Ver todas las integraciones</span>
                        </div>
                    </div>
            <tr>
<? if ($dni) { ?>
            <tr><td>CIF: </td>
            <td colspan="3"><?=$dni;?></td>
            </tr> <? ;} ?>  
<!--            <div class="panel-group " id="accordion" role="tablist" aria-multiselectable="true">
  <div class="panel panel-warning">
    <div class="panel-heading" role="tab" id="headingOne">
      <h4 class="panel-title">
        <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
          Collapsible Group Item #1
        </a>
      </h4>
    </div>
    <div id="collapseOne" class="panel-collapse collapse in" role="tabpanel" aria-labelledby="headingOne">
      <div class="panel-body">
        Anim pariatur cliche reprehenderit, enim eiusmod high life accusamus terry richardson ad squid. 3 wolf moon officia aute, non cupidatat skateboard dolor brunch. Food truck quinoa nesciunt laborum eiusmod. Brunch 3 wolf moon tempor, sunt aliqua put a bird on it squid single-origin coffee nulla assumenda shoreditch et. Nihil anim keffiyeh helvetica, craft beer labore wes anderson cred nesciunt sapiente ea proident. Ad vegan excepteur butcher vice lomo. Leggings occaecat craft beer farm-to-table, raw denim aesthetic synth nesciunt you probably haven't heard of them accusamus labore sustainable VHS.
      </div>
    </div>
  </div>
</div> 
-->
<!--	Botonera de acciones -->
<div id="extraCRM" class="row mb20">
<!--	Datos de la navegación del cupón ajax -->
<div class="">
			<span id="anterior">
            </span>
            <span id="posterior">
            </span>

<!--<div id="ocultar" class="col-lg-2 col-md-2 col-sm-2 pull-right">
    <form name="myform" method="post" action="ocultar.php">
        <input type="hidden" name="id" value="<?=$id;?>" />
        <button type="submit" name="ocultar"class="btn btn-danger" title="Ocultar"><i class="fa fa-thumbs-o-down fa-2x" aria-hidden="true"></i></button>
    </form>
</div>
-->    <div id="pedirTelefono" class="col-lg-2 col-md-2 col-sm-2 pull-right">
        <a href='envio_email_telefono.php?id=<?=$id?>&amp;keepThis=true&amp;TB_iframe=true&amp;height=150&amp;width=480' class='thickbox btn btn-success pedirTelefono'  target='_blank' title='Solicitar teléfono correcto'>
        <i class="fa fa-question fa-2x" aria-hidden="true"></i> <i class="fa fa-phone fa-2x" aria-hidden="true"></i> 
        <!--	Datos del envio del email pidiendo el teléfono ajax --> 
        <span id="emailtelefono">
        </span>
        </a> 
                             
    </div>
    <div id="spammer" class="col-lg-2 col-md-2 col-sm-2 pull-right">
        <a href="spammer.php?email=<?=$email;?>&amp;centro=<?=$fila->Centro;?>&amp;keepThis=true&amp;TB_iframe=true&amp;height=150&amp;width=480" title="Marcar como spammer" class='thickbox btn btn-danger' target='_blank'><i class="fa fa-user-times fa-2x" aria-hidden="true"></i></a>
    </div>
</div>
</div>

<!--	Notas colocadas al cupón --> 
<div id="notasBack" class="mb30 messages"></div>

<!--	Cupontrabajado en el Zoho --> 
<div id="cuponTrabajado" class="messages">
</div>

<!--	Panel de las respuestas de la encuesta 	-->
<div  class="panel panel-default" id="contenedorEncuesta">
    <div class="col-md-12"><h4>Resultados encuesta:</h4></div>
    
    <div class="panel-body" id="resultadoEncuesta">
    </div>
    <div  id="footerEncuesta" class="panel-footer panel-default clearfix">
        <button type="button" class="btn btn-primary pull-right" <?=$disabledsurvey= $contactId!=''?'':'disabled';?> id="enviarEncuesta">Enviar</button>
    </div>

</div>

<div class="campanas messages"><?=$campanas;?></div>
<!--	Comprobación de que el cupón ha sido anulado por algún centro anteriormente -->
<div class="cuponAnulado messages"></div>

<!--	Condiciones de traspaso -->
<div class="CondicionesTraspaso messages"></div>


<? if (($centroCupon=='52') && (requisitos_todosloscursos($nuevoid)!='')){?>
<div id="empresa">
    <div class="cupondata information" style="width:95%; margin:10px ">
    <?=modalidad_todosloscursos($nuevoid);?><br />
	<?=requisitos_todosloscursos($nuevoid);?>
    </div>
	<div class="clearer"></div>
</div>	
<? ;} ?>
<div id="notasCupon" class="mb30 messages"></div>
<div id="notaNew" class="mb30 panel panel-default">
	<div class="panel-body">
	<textarea class="form-control noresize" rows="3" id="notaCuerpo"></textarea>
     <div class="panel-footer panel-custom clearfix">
        <button type="button" class="btn btn-primary pull-right" id="sendNoteBack">Enviar</button>
        </div>
    </div>
</div>
<div id="stripjourneypanel" class="mb30 panel panel-default">
	<div class="panel-body">
	<textarea class="form-control noresize" rows="6" id="stripjourney"></textarea>
     <div class="panel-footer panel-custom clearfix">
        <button type="button" class="btn btn-primary pull-right" <?=$disabledjourney= $contactId!=''?'':'disabled';?> id="sendstripjourney">Enviar</button>
        </div>
    </div>
</div>

<!---		Cuadro de integraciones -->
<div id="integration" class="panel panel-default <?=$checkTraspaso = $traspaso==1 ? 'hidden' : '';?>" >
        <table class="table">
        <tr> 
<?=$tablaIntegraciones;?>
        </tr>
        </table>
</div>
                        
                        </div>
                        <!--	Panel con los datos extras del cupón / contact / potential -->
                <div class="col-lg-3 col-md-3 col-sm-6">
                    <div class="panel panel-info">
                        <div class="panel-body" >
                            
                            	<h4 class="text-center mb30"> <i class="fa fa-dot-circle-o"></i> Datos del zoho</h4>
                            <div class="row col-md-12 col-sm-12">
								<? //$contactId;?>
                                <div id="tenemosEncuesta" class="col-lg-3 col-md-3 col-sm-3 col-xs-3">
                                <span id="showEncuesta" title="Ver encuesta" class="btn btn-default btn-is-disabled"><i class="fa fa-commenting-o" aria-hidden="true"></i></span>
                                </div>
                                <div id="tenemosEncuesta" class="col-lg-3 col-md-3 col-sm-3 col-xs-3">
                                <a href="" class="btn btn-default btn-is-disabled" id="verEnZoho" target="_blank" title="Ver en zoho"> <i class="fa fa-user " aria-hidden="true"></i></a>
                                </div>
                                <div id="tenemosEncuesta" class="col-lg-3 col-md-3 col-sm-3 col-xs-3">
                                <span id="mostrarNotas" title="Notas CRM" class="btn btn-default btn-is-disabled"><i class="fa fa-bars" aria-hidden="true"></i> </span>
                                </div>
                                <div id="tenemosJourney" class="col-lg-3 col-md-3 col-sm-3 col-xs-3">
                                <span id="sendjourney" title="Enviar Journey" class="btn btn-default btn-is-disabled"><i class="fa fa-bars" aria-hidden="true"></i> </span>
                                </div>
                            </div>    
                        </div>
                     </div>
                        <!--		Journey del cupon	-->
                        <div class="col-lg-12 col-md-12 col-sm-12" id="journey">
                        
                        </div>
                        <div id="messageszoho" class="col-md-12">
                        
                        </div>
                </div>        
                    </div>
                </div>
            </div>

<div class="inplace-editor"></div>


<div class="clearer"></div>
 
    <div style="margin-right:20px; padding-top:10px; display:inline; float:right">
    	<span style="margin-right:170px;" id="navegacion">
            <? if ($contactId!='') { ?>        
            <? }; ?>
        </span>
        
	</div>    	
    </form>
</div>
<!--	Datos del multiple traspaso del cupon ajax --> 
<span id="multipletraspaso">
</span>
        
<!--	Cupones traspasados a Cumlaude -->
<div class="SituacionLaboralCumlaude"></div>

<!-- Integraciones -->
<div class="clearer playground"></div>
<!-- Integraciones end -->
</div>
</div>
</div>
</div>

<? //   echo 'nuevoid='.$nuevoid.'&NivelEstudios='.$NivelEstudios.'&SituacionLaboral='.$SituacionLaboral.'&Edad='.$edad.'&Provincia='.$provincia_id.'';?>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
<script src="//netdna.bootstrapcdn.com/bootstrap/3.3.2/js/bootstrap.min.js"></script>
<script type="text/javascript" src="../inc/js/thickbox.js"></script>	
<script type="text/javascript" src="../inc/js/jquery.editinplace.js"></script>
<script src="../src/a/inc/js/sweet-alert.js"></script>
<script src="../src/a/inc/js/pace.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.js"></script>

<script type="text/javascript">
/* Nuevas funciones */
	function cuponTrabajado(email,xpot){ //		Comprobamos si el cupón se está trabajando en el Zoho en este momento
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
			url:"../src/a/inc/cupones/cuponTrabajado.php",
			type: "POST",
			data: {email: email, xpot:xpot },
			dataType : "JSON",
			beforeSend: function () {
				$('#messageszoho').html('<i class="fa fa-cog fa-spin fa-3x fa-fw"></i><br> Comprobando datos...');
			},
            complete: function () {
				$('#messageszoho').html('operacion completa');
//					console.log($(opciones.sql));
 
				window.setTimeout(function () {
					$("#messageszoho").html('&nbsp;');
				}, 1000);
           },
			success: function(opciones){
				potentialid 		=	opciones.potentialid		!= null ? opciones.potentialid : '';
				module				=	potentialid 				!= '' ? 'Potentials' : 'Leads';
				contactid 			=	opciones.contactid			!= null ? opciones.contactid : '';
				if ((potentialid !='')||(contactid !='')){
				typepcontact		= 	potentialid					!= '' ? potentialid : contactid;
				$('#verEnZoho').attr('href', 'https://crm.zoho.com/crm/EntityInfo.do?module='+module+'&id='+typepcontact);
				$('#verEnZoho').addClass('btn-info');
				$('#verEnZoho').removeClass('btn-is-disabled','btn-default');
				} else {
					var contactInDB	=	'<?=$contactId;?>';
					if (contactInDB !=	'') {
						$('#verEnZoho').attr('href', 'https://crm.zoho.com/crm/EntityInfo.do?module=Leads&id='+contactInDB);
						$('#verEnZoho').addClass('btn-info');
						$('#verEnZoho').removeClass('btn-is-disabled','btn-default');
					}
				}
				motivonoventa		=	opciones.motivonoventa 	!= '' ? opciones.motivonoventa : 'Cupon abierto';
				producto			=	opciones.producto 		!= null ? opciones.producto : '';
				cerrado				=	opciones.cierre 			!= null ? '. Situación: <strong>'+opciones.cierre+'</strong>.' : '';
				if (potentialid != '') {
					$('#cuponTrabajado').addClass("alert alert-warning");
					$('#cuponTrabajado').html('<p>Traspasado a Zoho. Producto: <strong>' + producto +'</strong>'+cerrado+' ('+motivonoventa+')</p>');	
			}
			}
		})
	};
</script>
<script type="text/javascript">
/* Nuevas funciones */
//	function checkForPotential(contactid,email){ //		modificar el contactid por el potentialid
////		$('#messageszoho').addClass('.mensajeactivo');
//		
//		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
//			url:"../src/a/inc/cupones/contactToPotential.php",
//			type: "POST",
//			data: {contactid:contactid, email: email },
//			dataType : "JSON",
//			beforeSend: function () {
//				$('#messageszoho').html('<i class="fa fa-cog fa-spin fa-3x fa-fw"></i><br> Comprobando datos...');
//			},
//            complete: function () {
//				$('#messageszoho').html('operacion completa');
////					console.log($(opciones.sql));
// 
//				window.setTimeout(function () {
//					$("#messageszoho").html('&nbsp;');
//				}, 3000);
//           },
//			success: function(opciones){
//				alert (opciones.potentialid);
//				potentialid 			=	opciones.potentialid!= null ? opciones.potentialid : '';
//				motivonoventa		=	opciones.motivonoventa != '' ? opciones.motivonoventa : 'Cupon abierto';
//				producto			=	opciones.producto != null ? opciones.producto : '';
//				cerrado				=	opciones.cierre != null ? '. Situación: <strong>'+opciones.cierre+'</strong>.' : '';
//				if (potentialid		!=	'') {
//				$('#messageszoho').html('Cambiando contactid por potentialid');
//				}
//			}
//		})	
//	};
</script>
<script type="text/javascript">
/* Nuevas funciones */
	function notasBack(xpot,mode,nota){ //		
	console.log(xpot+'-'+mode+'-'+nota);
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
			url:"../src/a/inc/cupones/cuponesNotas.php",
			type: "POST",
			data: {xpot:xpot , mode:mode, nota:nota},
			dataType : "JSON",
			success: function(opciones){
				notas		 		=	opciones.nota;
				console.log(opciones.sql);
				if ((mode ='recuperar')&&(notas!= null)){
					$('#notasBack').html(notas); 
					$('#notasBack').addClass('alert alert-warning');
				}
				if (mode !='recuperar') {
				swal({title:"Nota enviada!", html: "<p>La nota se ha guardado correctamente</p>" ,type:"success"});
				}
			}
		})
	};
</script>
<script type="text/javascript">
/* Nuevas funciones */
	function notasCupon(seid){ //		Comprobamos si el cupón se está trabajando en el Zoho en este momento
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
			url:"../src/a/inc/ventas/notasCupon.php",
			type: "POST",
			data: {seid:seid },
			dataType : "JSON",
			success: function(opciones){
				notas		 		=	opciones.informacion;
				if (notas!='') {
					$('#notasCupon').html(notas); 
					$('#mostrarNotas').addClass('btn-info');
					$('#mostrarNotas').removeClass('btn-is-disabled','btn-default');
					$('#notasCupon').addClass('alert alert-warning');
}
			}
		})
	};
</script>
<script type="text/javascript">
/* Nuevas funciones */
	function encuestasCupon(id,email){ //		Comprobamos si el cupón ha contestado alguna encuesta
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
			url:"../src/a/inc/ventas/encuestasCupon.php",
			type: "POST",
			data: {id:id, email:email },
			dataType : "JSON",
			success: function(opciones){
//				alert('encuesta');
				var types = JSON.parse(JSON.stringify(opciones));
				for(x=0; x<types.length; x++) {
				//    console.log(types[x].pregunta);
				 //   console.log(types[x].respuesta);
					 idencuesta		=	types[0].encuesta;
					 encuestasend	=	types[0].send;
					 if ((types[x].respuesta !='') && (types[x].respuesta !=null)) {
						$('#resultadoEncuesta').append(types[x].pregunta +'<br>'+types[x].respuesta+'<br>');
						$('#showEncuesta').addClass('btn-info');
						$('#showEncuesta').removeClass('btn-is-disabled','btn-default');
					 }
				}
				$('#resultadoEncuesta').append('</div>');
				//alert (encuestasend);
				if (encuestasend == '1') {
				$('#footerEncuesta').addClass('footer-custom');
				$('#footerEncuesta').append('Encuesta enviada');
				}
//	console.log($('#resultadoEncuesta').html());
	console.log('Encuesta ' + idencuesta +' enviada: ' + encuestasend);
			}
		})
	};
</script>
<script type="text/javascript">
/* Nuevas funciones */
	function enviarNotas(contactid,notetitle,notecontent,kind){ //		Enviamos una nota al lead del Zoho
		console.log ('id='+contactid+'&notetitle='+notetitle+'&notecontent='+notecontent);
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
			url:"zohoAddNote.php",
			type: "POST",
			data: {id:contactid, notetitle:notetitle, notecontent:notecontent },
			dataType : "JSON",
			success: function(opciones){
				swal({title:"Información enviada!", html: "<p>Se ha enviado a Zoho de forma correcta</p>" ,type:"success"});
			}
		})
	};
</script>

<script type="text/javascript" async>
	function modificarDatos(id,element_id,update_value, recargar){ //		Enviamos una nota al lead del Zoho
		console.log ('Modificando '+element_id+' = '+update_value);
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=447702
			url:"guardar.php",
			type: "POST",
			data: {id:id, element_id:element_id, update_value:update_value },
			dataType : "JSON",
			success: function(opciones){
				if (recargar = true){
					swal({title:"Información enviada!", html: "<p>Cupón marcado como traspasado</p>" ,type:"success"});
					setTimeout(function(){location.reload();}, 1000);
				}
			}
		})
	};

</script>

<script type="text/javascript">
/* Nuevas funciones */
	function journey(xpot){ //		Recogemos el journey del cupón
		$.ajax({	//	http://www.tpm-corp.es/panel/editarCupones.php?id=00001
			url:"../src/a/inc/autopilot/journey.php",
			type: "POST",
			data: {xpot:xpot},
			dataType : "JSON",
			success: function(opciones){
				console.log (opciones);
				if (opciones.journey!= null){
					journey			=	'<ul class="milestones">'+opciones.journey+'</ul>';
					$("#journey").html(journey);
					$("#stripjourney").html(opciones.stripjourney);
					$("#sendjourney").removeClass('btn-is-disabled','btn-default');
					$("#sendjourney").addClass('btn-info');
				}
			}
		})
	};
</script>


<script type="text/javascript">
	$(document).ready(function() {
		var id			=	'<?=$id;?>';
		var idcentro		=	'<?=$centroCupon;?>';
		$.ajax({	//	Cargamos los datos todos los cupones que ha dejado los pintaremos en #cuponesLead
			url:"editarAjax.php",
			type: "GET",
			data: {id: id, idcentro: idcentro},
			dataType : "JSON",
			success: function(opciones){

				$("#Centro").html(opciones.marca);
				$("#ultimoid").html(opciones.ultimoid);
				$("#anterior").html(opciones.anterior);
				$("#posterior").html(opciones.posterior);
				if (opciones.emailtelefono != null) {
					$("#pedirTelefono").html('<i class="fa fa-check fa-2x" aria-hidden="true" style="color:green;"></i>');
				}
				$("#textoRepetido").html(opciones.textoRepetido);
	
				},
				error: function( jqXhr, textStatus, errorThrown ){
					console.log( errorThrown );
                }

			})
//		#Recuperación datos de ajax de la página#		//					
			
//		Comprobación de que los campos del cupón cumplen los requisitos del curso
		var NivelEstudios		=	'<?=$NivelEstudios;?>';
		var SituacionLaboral	=	'<?=$SituacionLaboral;?>';
		var	Edad				=	'<?=$edad;?>';
		var Provincia			=	'<?=$provincia_id;?>';
		var nuevoid				=	'<?=$nuevoid;?>';
		var sectorActividad		=	'<?=$sectorActividad;?>';
		
		$.ajax({	
			url:"../src/a/inc/cupones/requisitosCurso.php",
			type: "GET",
			data: {nuevoid : nuevoid, NivelEstudios: NivelEstudios, SituacionLaboral: SituacionLaboral, Edad: Edad, Provincia:Provincia, sectorActividad : sectorActividad },
			dataType : "JSON",
			success: function(opciones){
			$('.CondicionesTraspaso').html(opciones.traspasable);			
			},
			error: function( jqXhr, textStatus, errorThrown ){
				console.log( errorThrown );
                }

			})

//		Comprobación de si el cupón ha sido anulado por algún centro		
		$.ajax({	//	Enviamos los datos del centro para que se guarden en la BBDD
			url:"../src/a/inc/cupones/revisarCuponesAnulados.php",
			type: "POST",
			data: {Email: '<?=$email;?>'},
			dataType : "JSON",
			success: function(opciones){
				$(".cuponAnulado").html(opciones.mensaje);
			}
		})
//		Comprobamos si el cupón se encuentra en el Zoho
		cuponTrabajado 		('<?=$email;?>', '<?=$id;?>');
		<?=$llamanotas	=	$contactId!='' ? 'notasCupon ("'.$contactId.'");' : '' ;?>
		encuestasCupon 		('<?=$id;?>','<?=$email;?>');
		notasBack	 		('<?=$id;?>','recuperar');
		journey		 		('<?=$id;?>');


//		EditInPlace								//
		$("#Email").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Curso").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Nombre").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Apellidos").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Edad").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});
		
		$("#Telefono").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Direccion").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Piso").editInPlace({
		default_text: "",
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Puerta").editInPlace({
		default_text: "",
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

		$("#Poblacion").editInPlace({
		default_text: "",
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});
		$("#Cp").editInPlace({
		default_text: "",
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

<?php 
$sql = "SELECT * FROM `NivelEstudios` WHERE `Id` > 10 LIMIT 0 , 30";
$rs = mysql_query($sql,$link); 
$num_registros = mysql_num_rows($rs);
$fila = mysql_fetch_array($rs);
	$numero= 0;
	$estudios2='';
while ($fila){ 
	if ($estudios2 == ''){
	$estudios2 = utf8_decode($fila[1]); } else {
		$estudios2 = $estudios2.', '.utf8_decode($fila[1]); 
		}
	$fila=mysql_fetch_array($rs); 
  }
?>
		$("#NivelEstudios").editInPlace({
		default_text: "",
		url: "guardar.php",
		field_type: "select",
		params: "id=<?=$id?>", 
		select_options: "<?=utf8_encode($estudios2) ;?>"
		});

		$("#Empresa").editInPlace({
		url: "guardar.php",
		params: "id=<?=$id?>", 
		});

$("#Test").editInPlace({
		default_text: "",
		url: "guardar.php",
		field_type: "select",
		params: "id=<?=$id?>", 
		select_options: "Si, No"
		});

$("#Centro").editInPlace({
		default_text: "",
		url: "guardar.php",
		field_type: "select",
		params: "id=<?=$id?>", 
		select_options: "Lazarus, TPM - Bonificada, TPM - Privada sin Precio, TPM - Privada con precio, TPM - Bonificada Premium"
		});
		
$("#SituacionLaboral").editInPlace({
		default_text: "",
		url: "guardar.php",
		field_type: "select",
		params: "id=<?=$id?>", 
		select_options: "Desempleado, Estudiante, Trabajador por cuenta ajena, Autónomo, Empresario, Jubilado, No declarada, Funcionario"
		});
		$(".mostrar").click(function () {
			$("#hint1").toggle("slow");
		});  
		$('#mostrarNotas').click(function() {
			$("#notasCupon").toggle("slow");
		});
//	Mostrar/ocultar las integraciones
		$('#verIntegraciones').click(function() {
			$('#integration').removeClass('hidden');
			$('#verIntegraciones').addClass('hidden');
		});
		
//	Mostrar/ocultar resultados encuesta
		$('#showEncuesta').click(function() {
			$("#resultadoEncuesta").toggle("fast");
			$('#contenedorEncuesta').toggle();
			$("#enviarEncuesta").toggle();
			$('.messages').toggle();
		});	

//	Mostrar/ocultar notas del back
		$('#verNotasBack').click(function() {
			console.log('pulsado #verNotasBack');
			$("#notaNew").toggle('fast');
		});	

//	Mostrar/ocultar sendjourneystrip
		$('#sendjourney').click(function() {
			console.log('pulsado #sendjourney');
			$("#stripjourneypanel").toggle('fast');
		});	

//	Enviar notas
		$('#sendNoteBack').click(function() {
			notas		=	$("#notaCuerpo").val();
			console.log("#notaCuerpo = "+notas);
			mode		=	'insertar';
			xpot		=	'<?=$id;?>';
			notasBack(xpot,mode,notas);
			$("#notaCuerpo").val();
			$('#notaNew').toggle();
		});	
		
		$('.closer').click(
			function(){
				$($(this).attr('href')).slideUp('fast');
				return false;
			}
		);
		$("#hint1").toggle();


//	Marcar el cupón como traspasado
		$('#marcarTraspasadoTPM').click(function() {
			console.log('pulsado #marcarTraspasadoTPM');
			
			var id 		= 	'<?=$id;?>';
			modificarDatos (id,'Traspaso','1',false);
			modificarDatos (id,'Integraciones','0',true);
			
			});	
		

});	
</script>
<script>
/* Previenen el comportamiento por defecto y llaman a las paginas que desmarcan el cupon, tanto por doble como por marca */
$(function() {
   $(".alerta a").click(function(event) {
    event.preventDefault();
 	 $(".alerta").load(this.href);
   });
   $("a.desmarcar_cupon").click(function(event) {
    event.preventDefault();
 	 $(".playground").load(this.href);
   });

 });

/* 	Enviamos la encuesta al contactId que tengamos	*/
$('#enviarEncuesta'). click(function(event) {
	var	contactId				=	'<?=$contactId?>'
	var notecontent				=	$('#resultadoEncuesta').html();
	var notetitle				=	'El usuario ha contestado una encuesta';
	var	kind					=	'survey';
//	alert (notecontent);
	if (contactId !='') {
		enviarNotas(contactId,notetitle,notecontent,kind);
	} else {
		alert ('No hay vinculado ningún contacto a este cupón');
	}
});

	
/* 	Enviamos la journey al contactId que tengamos	*/
$('#sendstripjourney'). click(function(event) {
	var	contactId				=	'<?=$contactId?>'
	var notecontent				=	$('#stripjourney').html();
	var notetitle				=	'Actividad del usuario';
	var	kind					=	'journey';
//	alert (notecontent);
	if (contactId !='') {
		enviarNotas(contactId,notetitle,notecontent,kind);
	} else {
		alert ('No hay vinculado ningún contacto a este cupón');
	}
});

//	Sirve para que todos los cupones tengan la misma situación laboral que este cupón
$("#igualar").click(function(event) {
    event.preventDefault();
// 	 alert ('igualar todas las situaciones laborales');
	 var SituacionLaboral 		= 	'<?=$SituacionLaboral;?>';
	 var Email					=	'<?=$email?>';
	 //$(".alerta").load(this.href);
	$.ajax({	
	url:"../src/a/inc/cupones/igualarSituacionLaboral.php",
	type: "GET",
	data: {SituacionLaboral : SituacionLaboral, Email : Email },
	dataType : "JSON",
	success: function(opciones){
//		alert (opciones.query);
		if (opciones.query = true) { 
			location.reload(true);
		}
	},
	error: function( jqXhr, textStatus, errorThrown ){
		console.log( errorThrown );
		}

	})

   });
   
$("#igualar").hover(function(e) {
    $(".igualarspin").addClass('fa-spin');
}, function() {
    $(".igualarspin").removeClass('fa-spin');
});   
$(".navbar-brand").hover(function(e) {
    $("#superb").addClass('fa-spin');
}, function() {
    $("#superb").removeClass('fa-spin');
});   
</script>

<? 
if (isset($_REQUEST['viewed']) && $_REQUEST['viewed'] == true) {		
// 						En el caso de que tengamos mensajes nos preparamos para mostrarlos u ocultarlos
	?>
<script>

toastr.options = {
  "closeButton": true,
  "debug": false,
  "newestOnTop": true,
  "progressBar": true,
  "positionClass": "toast-bottom-right",
  "preventDuplicates": false,
  "showDuration": "300",
  "hideDuration": "1000",
  "timeOut": "4000",
  "extendedTimeOut": "1000",
  "showEasing": "swing",
  "hideEasing": "linear",
  "showMethod": "show",
  "hideMethod": "fadeOut"
}
	muteMessages('desactivar');
	toastr.options.onclick = function() { console.log('clicked'); muteMessages('activar'); }
//	toastr.options.onHidden = function() { console.log('goodbye');  }				
	toastr["success"]("Desactivando notificaciones del cupón");
				
function muteMessages(action){
	var	id		=	'<?=$id;?>';
	var action	= 	action;	
//	alert (action);
	$.ajax({	//	Cargamos los mensaje que tengamos activos en el back
		url:"../src/a/inc/panel/journeyMessages.php",
		type: "POST",
		data: {id : id, action: action },
		dataType : "JSON",
		success: function(opciones){
			if (action == 'activar'){
			toastr["success"]("Las notificaciones seguirán apareciendo");
			}
//			alert (opciones.sql);
		}
		});
};


</script>
<? ;}?>

 <script>
 
$.fn.refreshMe = function(opts){
  
      var $this = this,
          defaults = {
            ms:1500,
            parentSelector:'.panel',
            started:function(){},
            completed:function(){}
          },
          settings = $.extend(defaults, opts);
  
      var par = this.parents(settings.parentSelector);
      var panelToRefresh = par.find('.refresh-container');
      var dataToRefresh = par.find('.refresh-data');
      
      var ms = settings.ms;
      var started = settings.started;		//function before timeout
      var completed = settings.completed;	//function after timeout
      
      $this.click(function(){
        $this.addClass("fa-spin");
        panelToRefresh.show();
        if (dataToRefresh) {
          started(dataToRefresh);
        }
        setTimeout(function(){
          if (dataToRefresh) {
              completed(dataToRefresh);
          }
          panelToRefresh.fadeOut(800);
          $this.removeClass("fa-spin");
        },ms);
        return false;
      })//click
      
}/* end function refreshMe */

$(document).ready(function(){
});
</script>
</body>
</html>
