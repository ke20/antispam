
Mod: antispam
Author: Kevin AUVINET

HOW TO INSTALL:

-- 
	1 - Add folders French and English in the "lang" directory
--

*******************************

--
-- Open register.php -- 

	1 - Find line which contains "require PUN_ROOT.'lang/'.$pun_user['language'].'/prof_reg.php';"
	
	2 - After, paste the code below:
	
		require PUN_ROOT.'lang/'.$pun_user['language'].'/antispam.php';
		
	3 - Find line which contains "if (isset($_POST['form_sent']))"
	
	4 - In the condition, paste the code below:
	
		$service_url = 'http://www.stopforumspam.com/api' . 
        $service_url.= '?email='.strtolower(pun_trim($_POST['req_email1']));
        $service_url.= '&f=json';
        $fContent = file_get_contents($service_url);
        $jsonValue = json_decode($fContent);
        if($jsonValue->email->frequency > 0 
        && $jsonValue->email->appears > 0)
                message($lang_antispam['Is spamer']);
				

-- Close register.php 
--


