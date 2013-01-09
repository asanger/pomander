<?php

if(!class_exists("\\Pomander"))
{
	try {
		$dir = dirname(dirname(__DIR__));
		require_once "{$dir}/autoload.php";
	}catch(Exception $e)
	{
		echo "Failed to load Pomander library. Is pom installed in the proper location?\n";
	}
}

// get the task list
$args = $GLOBALS['argv'];
array_splice($args, 0, 3);
$parser = new \Pomander\OptionParser($args);
$tasks = array();

foreach($parser->get_non_options() as $option)
	if(strpos($option, '=') === false) $tasks[] = $option;

// set our top level tasks and lib
$app = phake\Builder::$global->get_application();
$app->top_level_tasks = count($tasks)? $tasks : array('default');
$app->dir = __DIR__.'/lib';

// load Pomander/Pomfile
$runfile = \Pomander::resolve_runfile(getcwd());
if(!$runfile)
{
	$pom = new \Pomander\Builder();
	$pom->run();
}else
{
	phake\load_runfile($runfile);
}
