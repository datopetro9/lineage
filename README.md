lineage
=======
                                          <!   Server Status ON/OFF />
                                          
                                          
 <?php
  $server_ip = "localhost";
  $loginserver_port = "7777";
  $gameserver_port = "2106";

  $login_status = @fsockopen( "$server_ip" , "$loginserver_port", $errno, $errstr, 0);
  $game_status = @fsockopen( "$server_ip" , "$gameserver_port", $errno, $errstr, 0);
   
  if($login_status){
  echo"Login:&nbsp;&nbsp;&nbsp;Online<br />";
   }
  else{
  echo"Login::&nbsp;&nbsp;&nbsp;Offline<br />";   
   }
   if($game_status){
      echo" Game:&nbsp;&nbsp;&nbsp;Online<br />";
   }
   else{
      echo" Game:&nbsp;&nbsp;&nbsp;Offline<br />";
   };
mysql_close($connect);
?>                                




                                          <!   Players Online />
                                          (მაგალითად: სულ ონლაინშია 25 კაცი)
                                          
<?php
   $server_ip = "localhost";
   $mysql_user = "";
   $mysql_pass = "";
   $database = "";
   
   $connect = mysql_connect("$server_ip", "$mysql_user", "$mysql_pass") or die(mysql_error()); 
   $db_select = mysql_select_db("$database", $connect) or die(mysql_error());
   $query = mysql_query("SELECT online FROM characters WHERE online=1") or die(mysql_error()) ;
   
   $online_chars = mysql_num_rows($query);
   
   echo 'Players Online:'.$online_chars;
   
mysql_close($connect);
?>



                                          <!   GM LIST />
                                          (მაგალითად:  [GM]Petro [Online]   /  [GM]David [Offline]
                                      
 <?php
   $server_ip = "localhost";
   $mysql_user = "";
   $mysql_pass = "";
   $database = "";
   
   $connect = mysql_connect("$server_ip", "$mysql_user", "$mysql_pass") or die(mysql_error()); 
   $db_select = mysql_select_db("$database", $connect) or die(mysql_error());
   $gm_list = mysql_query("SELECT char_name,accesslevel,online FROM characters WHERE accesslevel>=1") or die(mysql_error()) ;
   
  echo'<table border="0">';
  while($row=mysql_fetch_array($gm_list)){
  $nick = $row['char_name'];
  $online = $row['online'];
  if($online == 1){
  $online = 'Online';
  }else{
  $online = 'Offline';
  }
  echo'<tr><td>'.$nick.'</td><td>['.$online.']</td></tr>';
      
   }
   echo'</table>';
   mysql_close($connect);

?>



                                          <!   Account and Characters Created />
                                          (მაგალითად: სულ შექმნილია: 25 პერსონაჟი  /  8 ექაუნთი)
                                          
 <?php
   $server_ip = "localhost";
   $mysql_user = "root";
   $mysql_pass = "";
   $database = "test";
   
   $connect = mysql_connect("$server_ip", "$mysql_user", "$mysql_pass") or die(mysql_error()); 
   $db_select = mysql_select_db("$database", $connect) or die(mysql_error());
   $characters = mysql_query("SELECT * FROM characters") or die(mysql_error()) ;
   $accounts = mysql_query("SELECT * FROM accounts") or die(mysql_error()) ;
   
   $total_char = mysql_num_rows($characters);
   $total_acc = mysql_num_rows($accounts);
   
   echo 'Characters created:&nbsp;'.$total_char.'</br>';
   echo 'Accounts created:&nbsp;'.$total_acc;
   
mysql_close($connect);
?>
