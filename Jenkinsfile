pipeline {
  agent any
  stages {
    stage('') {
      steps {
        powershell(script: '$commit_head=git log $commit_head_1=$commit_head.Split([Environment]::NewLine) | Select -First 1   $get_id=($commit_head_1.Split(" "))[1] echo "################# $get_id #########################"  echo "#### Creating File only if it doesn\'t exist ###" $check_file = Test-Path -path $ENV:WORKSPACE\\commit_id.log $trigger_file = Test-Path -path $ENV:WORKSPACE\\trigger_dependency_file.log $mail = Test-Path -path $ENV:WORKSPACE\\mail.log  $ENV:Git_Branch>branch.txt Get-Content .\\branch.txt | out-file -encoding ASCII branchAscii.txt  if ($check_file -eq "True"){ echo "################# File is already there, so cool #########################" } else { echo "################# Creating file to save commitID #########################" ni $ENV:WORKSPACE\\commit_id.log -type file }  $var_id=$(Get-Content $ENV:WORKSPACE\\commit_id.log)  echo "created commit ID as variable" echo $var_id  if ($get_id -eq "$var_id"){ echo "#######################################################################################" echo "##########  No Commits Found ): Skipping Build, Sit Back and Breath Heavily ###########" echo "#######################################################################################"  if ($trigger_file -eq "True"){ echo "################# File is already there, so cool #########################" rm -r $ENV:WORKSPACE\\trigger_dependency_file.log ni $ENV:WORKSPACE\\mail.log -type file else if { echo "################# File doesn\'t exist, be cool #########################" } } } else { echo "##############################################################################################" echo "#################  Generating Build, (: Sit Properly and Get Ready To Fix Bugs ###############" echo "##############################################################################################" ni $ENV:WORKSPACE\\trigger_dependency_file.log -type file rm -r $ENV:WORKSPACE\\mail.log } echo $get_id $get_id>$ENV:WORKSPACE\\commit_id.log echo "redirecting $get_id out put to $ENV:WORKSPACE\\commit_id.log"', label: 'powershell', returnStatus: true, returnStdout: true)
      }
    }
  }
}