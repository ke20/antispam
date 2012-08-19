Mod: antispam
Auteur: Kevin AUVINET

INSTALLATION:

-- 
	1 - Ajouter les dossiers "French" et "English" dans le dossier "lang"
--

*******************************

--
-- Ouvrez register.php -- 

	1 - Trouvez la ligne contenant "require PUN_ROOT.'lang/'.$pun_user['language'].'/prof_reg.php';"
	
	2 - Après cette ligne, copiez le code ci-dessous:
	
		require PUN_ROOT.'lang/'.$pun_user['language'].'/antispam.php';
		
	3 - Trouvez la ligne contenant "if (isset($_POST['form_sent']))"
	
	4 - Dans la condition, collez le code ci-dessous:
	
		$service_url = 'http://www.stopforumspam.com/api' . 
        $service_url.= '?email='.strtolower(pun_trim($_POST['req_email1']));
        $service_url.= '&f=json';
        $fContent = file_get_contents($service_url);
        $jsonValue = json_decode($fContent);
        if($jsonValue->email->frequency > 0 
        && $jsonValue->email->appears > 0)
                message($lang_antispam['Is spamer']);
				

-- Fermez register.php 
--