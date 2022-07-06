@Library('jenkins library') _
def tool = new org.devops.tools()

String workspace= "D:/Program Files/Jenkins workspace"

pipeline{
    agent {    
        node{
            label "demo"  //指定运行节点的的标签
            customWorkspace "${workspace}"  //指定运行工作目录可自定义
        }
    }
  options{
      timestamps()  //日志会有时间
      skipDefaultCheckout()  //删除隐式checkout scm语句
      disableConcurrentBuilds()  //禁止并行
      timeout(time: 1,unit: 'HOURS')  //流水线超时设置1h
      
  }
  stages{
       //下载代码
       stage("GetCode"){  //阶段名称
          steps{  //步骤
              timeout(time:5,unit:"MINUTES"){ //步骤超时时间
                script{  //填写运行代码
                    print('获取代码')
                }
            }
        }
      }
      //构建
      stage("Build"){
           steps{
              timeout(time:20,unit:"MINUTES"){
                script{
                     print('应用打包')
                }  
              }
          }
      }
      //代码扫描
      stage("CodeScan"){
           steps{
              timeout(time:30,unit:"MINUTES"){
                script{
                     print('代码扫描')
                  tools.PrintMes("this is my library!")
                }  
              }
          }
      }
  }
  //构建后操作
  post {
      always {
            script{
                println("always")
            }
       }
       success {
            script{
                currentBuild.description += "\n 构建成功"
            }
       }
       failure {
            script{
                currentBuild.description += "\n 构建失败"
            }
       }
       aborted {
            script{
                currentBuild.description += "\n 构建取消"
            }
       }
  }
    
}
  
