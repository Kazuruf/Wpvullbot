<?php
header("Content-type: text/html; charset=utf-8");



function wpversion($wpbot){
  
  if($wpbot=="Wordpress4.7"){
    $out = "Vull 4.7 :\n";
  $urli = file_get_contents("https://wpvulndb.com/api/v2/wordpresses/47");
  $resultado = json_decode($urli, true);
  foreach($resultado['4.7']['vulnerabilities'] as $resultx){
  $out .= "\n";
  $out .= "Vull: ".$resultx['title']."\n";
  $out .= "URL: ". $resultx['references']['url']['0'] ."\n";
  $out .= "URL: ". $resultx['references']['url']['1'] ."\n";
  $out .= "Tipo Vull: " .$resultx['vuln_type'] ."\n";
  $out .= "Versão: " .$resultx['fixed_in'] ."\n";}
}

elseif ($wpbot =="Wordpress4.6"){
$urli = file_get_contents("https://wpvulndb.com/api/v2/wordpresses/46");
  $resultado = json_decode($urli, true);
  foreach($resultado['4.6']['vulnerabilities'] as $resultx){
  $out .= "\n";
  $out .= "Vull: ".$resultx['title']."\n";
  $out .= "URL: ". $resultx['references']['url']['0'] ."\n";
  $out .= "URL: ". $resultx['references']['url']['1'] ."\n";
  $out .= "Tipo Vull: " .$resultx['vuln_type'] ."\n";
  $out .= "Versão: " .$resultx['fixed_in'] ."\n";}
}

elseif ($wpbot =="Wordpress4.5"){
$urli = file_get_contents("https://wpvulndb.com/api/v1/wordpresses/45");
  $resultado = json_decode($urli, true);
  foreach($resultado['wordpress']['vulnerabilities'] as $resultx){
  $out .= "\n";
  $out .= "Vull: ".$resultx['title']."\n";
  $out .= "URL: ". $resultx['url']['0']."\n";
  $out .= "Tipo Vull: " .$resultx['vuln_type'] ."\n";
  $out .= "Versão: " .$resultx['fixed_in'] ."\n";}
}

elseif ($wpbot =="Wordpress4.4"){
$urli = file_get_contents("https://wpvulndb.com/api/v1/wordpresses/44");
  $resultado = json_decode($urli, true);
  foreach($resultado['wordpress']['vulnerabilities'] as $resultx){
  $out .= "\n";
  $out .= "Vull: ".$resultx['title']."\n";
  $out .= "URL: ". $resultx['url']['0']."\n";
  $out .= "Tipo Vull: " .$resultx['vuln_type'] ."\n";
  $out .= "Versão: " .$resultx['fixed_in'] ."\n";}
}

else {
  $out .= "Erro !";

}
  return $out;

}


define('BOT_TOKEN', 'TOKEN');
define('API_URL', 'https://api.telegram.org/bot'.BOT_TOKEN.'/');

function processMessage($message) {
  $message_id = $message['message_id'];
  $chat_id = $message['chat']['id'];
  if (isset($message['text'])) {
    $text = $message['text'];
    if (strpos($text, "/start") === 0) {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => 'Olá, '. $message['from']['first_name'].
    ' sou um BOT que pesquisa e informa as vulnerabilidades existente nas versões do  Wordpress, baseado nos principais sites de Exploits. Usaremos as versões acima da 4.4 . ', 'reply_markup' => array(
        'keyboard' => array(array('Wordpress4.7', 'Wordpress4.6'), array('Wordpress4.5', 'Wordpress4.4'), array('Temas', 'Sobre')),
        'one_time_keyboard' => true)));
    } else if ($text === "Wordpress4.7") {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => wpversion('Wordpress4.7', $text)));
    }
else if ($text === "Wordpress4.6") {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => wpversion('Wordpress4.6', $text)));
    }
    else if ($text === "Wordpress4.5") {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => wpversion('Wordpress4.5', $text)));
    }
    else if ($text === "Wordpress4.4") {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => wpversion('Wordpress4.4', $text)));
    }
    else if ($text === "Temas") {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => "Em breve..."));
    }
 else if ($text === "Sobre") {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => '
        Bot para verificar vulnerabilidades em versões do Wordpress. 
Em breve: Plugins e Temas. 
Autor: Mateus Alves - HatBash Br

'));
    } else {
      sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => 'Erro !'));
    }
  } else {
    sendMessage("sendMessage", array('chat_id' => $chat_id, "text" => 'Somente texto.'));
  }
}
function sendMessage($method, $parameters) {
  $options = array(
  'http' => array(
    'method'  => 'POST',
    'content' => json_encode($parameters),
    'header'=>  "Content-Type: application/json\r\n" .
                "Accept: application/json\r\n"
    )
);
$context  = stream_context_create( $options );
file_get_contents(API_URL.$method, false, $context );
}
$update_response = file_get_contents("php://input");
$update = json_decode($update_response, true);
if (isset($update["message"])) {
  processMessage($update["message"]);
}

?>




