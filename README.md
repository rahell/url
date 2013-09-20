<?php
/**
 * onArcade 2.4.0
 * Copyright © 2006-2011 Hans Mäesalu & Eveterm OÜ, All Rights Reserved
 **
 * ONARCADE IS NOT FREE SOFTWARE!
 * http://www.onarcade.com
 **
 * URLs generating class
 **/
class URL {

	var $replace = array(' ', '\'', ':', '(', ')', '&', 'ä', 'ö', 'ü', 'õ', '?');

	var $replacement = array('_', '', '-', '8', '9', 'and', 'a', 'o', 'y', 'o', '');

	var $site_url;

	var $search_engine_friendly;

	var $file_url;

	var $category_url;

	var $profile_url;

	function URL($site_url, $search_engine_friendly, $file_url, $category_url, $profile_url) {
		$this->site_url = $site_url;
		$this->search_engine_friendly = ($search_engine_friendly == 1);
		$this->file_url = $file_url;
		$this->category_url = $category_url;
		$this->profile_url = $profile_url;
		$this->scores_url = $scores_url;
	}

	function file($id, $title) {
		if ($this->search_engine_friendly) {
			            return $this->site_url .'/'. $id .'.html'; 
		} else {
			return $this->site_url .'/file.php?f='. $id;
		}
	}

	function category($id, $title, $page = 1, $order = 'title') {
		if ($this->search_engine_friendly) {
                  return $this->site_url .'/'. $this->category_url . $id
                . ($order !== 'title' ? '/'. $order : '')
                . ($page > 1 || $order !== 'title' ? '/'. $page .'.html' : ''); 
		} else {
			return $this->site_url .'/browse.php?c='. $id .'&amp;p='. $page . ($order === 'title' ? '' : '&amp;order='. $order);
		}
	}

	function profile($id, $username) {
		if ($this->search_engine_friendly) {
			$username = str_replace($this->replace, $this->replacement, $username);
			return $this->site_url .'/'. $this->profile_url .'/'. $id .'/'. $username .'.html';
		} else {
			return $this->site_url .'/profile.php?u='. $id;
		}
	}

	function tag($tag, $page = 1, $category = 0, $order = 'relevance') {
		return $this->site_url .'/search.php?t='. urlencode($tag) . ($page > 1 ? '&amp;p='. $page : '') . ($category !== 0 ? '&amp;c='. $category : '') . ($order === 'relevance' ? '' : '&amp;order='. $order);
	}

}

?>
