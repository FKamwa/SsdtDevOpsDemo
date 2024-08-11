pipeline { 
    agent any
    stages{
    stage('git checkout') {
        steps {
        //git 'file:///C:/Projects/SsdtDevOpsDemo'
        git 'https://github.com/FKamwa/SsdtDevOpsDemo.git'
        }
    }
 /*   stage('Clean Workspace'){
        steps{
            cleanWs()
        }
    } */
    stage('Build Dacpac from SQLProj') {
        steps{
        bat "\"${tool name: 'Default', type: 'msbuild'}\" /p:Configuration=Release"
        stash includes: 'SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac', name: 'theDacpac' }
    }
 
    stage('Deploy Dacpac to SQL Server') {
        steps{
        unstash 'theDacpac'
        bat "\"C:\\Program Files (x86)\\Microsoft SQL Server\\140\\DAC\\bin\\sqlpackage.exe\" /Action:Publish /SourceFile:\"SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac\" /TargetServerName:(local) /TargetDatabaseName:Chinook"    }
}
    }}
