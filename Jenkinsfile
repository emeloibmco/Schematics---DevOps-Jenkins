

pipeline {
    agent any
    parameters{
            booleanParam(name: 'Linux', defaultValue: false, description:'Seleccione este campo si su Jenkins corre en Linux')
    }

    stages {
        stage("IBM Schematics") {
            steps {
                script{
// LINUX 
                    if(params.Linux == true){
                    sh ''' 
                    token="eyJraWQiOiIyMDIwMDYyNDE4MzAiLCJhbGciOiJSUzI1NiJ9.eyJpYW1faWQiOiJJQk1pZC01NTAwMDVBQTY2IiwiaWQiOiJJQk1pZC01NTAwMDVBQTY2IiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjU1MDAwNUFBNjYiLCJnaXZlbl9uYW1lIjoiTGF1cmEgSnVsaWFuYSIsImZhbWlseV9uYW1lIjoiTGXDs24gR29uesOhbGV6IiwibmFtZSI6IkxhdXJhIEp1bGlhbmEgTGXDs24gR29uesOhbGV6IiwiZW1haWwiOiJsanVsaWFuYWxAaWJtLmNvbSIsInN1YiI6ImxqdWxpYW5hbEBpYm0uY29tIiwiYWNjb3VudCI6eyJ2YWxpZCI6dHJ1ZSwiYnNzIjoiZDc1NmE2YWVmMGVkNGQxOGFkNDNhYTcwY2ZlZjAzM2QiLCJpbXNfdXNlcl9pZCI6IjgxOTc0MjgiLCJpbXMiOiIyMDU5Mzg2In0sImlhdCI6MTU5NDgyNDY1OSwiZXhwIjoxNTk0ODI4MjU5LCJpc3MiOiJodHRwczovL2lhbS5jbG91ZC5pYm0uY29tL2lkZW50aXR5IiwiZ3JhbnRfdHlwZSI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJpYm0gb3BlbmlkIiwiY2xpZW50X2lkIjoiYngiLCJhY3IiOjEsImFtciI6WyJwd2QiXX0.Cw4KNIZNht4BF0EIg3pWXhCgn8jhDt0FZzNPxAesXQdTiHHXWfTgXAAEITxwVFjFHR96uJ55N6zyNzKv6ZLJfNc_eaba6NGFznfrsUn9fhs4T-JlNzjgxew5032A28Ls34gXBBwTUWTekRvh-USftgQAXM9Gz0dMRaMTGD7VL6XBNJoet6z64zXrtE3qZyCR_dUkDGx3y-KMc4BqN3J8B-skhbX_229HTylYAK7FmwdgBwl_YMmgZjUUh2XaqGJDpQOs6QaMFyN0Z7UjRhA8kGS76f4GOch2MQSrG9UVWF9E1IbuiUdYQE5ZnH0zrDwPdEPM3VIU9uTt9Sok4-Q8dg"
                    id=$(curl --request POST --url https://schematics.cloud.ibm.com/v1/workspaces -H "Authorization: $token" -d '{"name":"jenkins","type": ["terraform_v0.12"],"location": "us-east","description": "Demo","resource_group": "Default","tags": [],"template_repo": {"url": "https://github.com/emeloibmco/Skytap-DevOps-Terraform"},"template_data": [{"folder": ".","type": "terraform_v0.12","variablestore": [{"name": "username","value": "Mario.Olarte@ibm.com"},{"name": "api_token","value": "6115ade86dd67520095a252554744e0d09adc956"}]}]}' | grep -Eo "(jenkins-[0-9a-z-]*)" | tail -n 1) 
                    echo "WorkSpace creado!"              
                    echo $id
                    sleep 10
                    curl -X POST https://schematics.cloud.ibm.com/v1/workspaces/$id/plan -H "Authorization: $token" -H "refresh_token: $token"
                    echo "Plan creado!" 
                    '''

                    /* sleep 40
                    curl -X PUT https://schematics.cloud.ibm.com/v1/workspaces/$id/apply -H "Authorization: $token" -H "refresh_token: $token"
                    echo "Plan aplicado!"
                    curl -X PUT https://schematics.cloud.ibm.com/v1/workspaces/jenkins-57c7c629-83ee-40/destroy -H "Authorization: $token" -H "refresh_token: $token"
                    echo "Plan destruido!" */
                }

// WINDOWS
                else{
                    powershell '''
                    $token="eyJraWQiOiIyMDIwMDYyNDE4MzAiLCJhbGciOiJSUzI1NiJ9.eyJpYW1faWQiOiJJQk1pZC01NTAwMDVBQTY2IiwiaWQiOiJJQk1pZC01NTAwMDVBQTY2IiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjU1MDAwNUFBNjYiLCJnaXZlbl9uYW1lIjoiTGF1cmEgSnVsaWFuYSIsImZhbWlseV9uYW1lIjoiTGXDs24gR29uesOhbGV6IiwibmFtZSI6IkxhdXJhIEp1bGlhbmEgTGXDs24gR29uesOhbGV6IiwiZW1haWwiOiJsanVsaWFuYWxAaWJtLmNvbSIsInN1YiI6ImxqdWxpYW5hbEBpYm0uY29tIiwiYWNjb3VudCI6eyJ2YWxpZCI6dHJ1ZSwiYnNzIjoiZDc1NmE2YWVmMGVkNGQxOGFkNDNhYTcwY2ZlZjAzM2QiLCJpbXNfdXNlcl9pZCI6IjgxOTc0MjgiLCJpbXMiOiIyMDU5Mzg2In0sImlhdCI6MTU5NDgyNDY1OSwiZXhwIjoxNTk0ODI4MjU5LCJpc3MiOiJodHRwczovL2lhbS5jbG91ZC5pYm0uY29tL2lkZW50aXR5IiwiZ3JhbnRfdHlwZSI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJpYm0gb3BlbmlkIiwiY2xpZW50X2lkIjoiYngiLCJhY3IiOjEsImFtciI6WyJwd2QiXX0.Cw4KNIZNht4BF0EIg3pWXhCgn8jhDt0FZzNPxAesXQdTiHHXWfTgXAAEITxwVFjFHR96uJ55N6zyNzKv6ZLJfNc_eaba6NGFznfrsUn9fhs4T-JlNzjgxew5032A28Ls34gXBBwTUWTekRvh-USftgQAXM9Gz0dMRaMTGD7VL6XBNJoet6z64zXrtE3qZyCR_dUkDGx3y-KMc4BqN3J8B-skhbX_229HTylYAK7FmwdgBwl_YMmgZjUUh2XaqGJDpQOs6QaMFyN0Z7UjRhA8kGS76f4GOch2MQSrG9UVWF9E1IbuiUdYQE5ZnH0zrDwPdEPM3VIU9uTt9Sok4-Q8dg"
                    $id=(Invoke-RestMethod -Uri "https://schematics.cloud.ibm.com/v1/workspaces" -Method "Post" -Headers @{"Authorization" = $token} -Body \'{"name":"jenkins","type": ["terraform_v0.12"],"location": "us-east","description": "Demo","resource_group": "Default","tags": [],"template_repo": {"url": "https://github.com/emeloibmco/Skytap-DevOps-Terraform"},"template_data": [{"folder": ".","type": "terraform_v0.12","variablestore": [{"name": "username","value": "Mario.Olarte@ibm.com"},{"name": "api_token","value": "6115ade86dd67520095a252554744e0d09adc956"}]}]}\').id
                    echo $id
                    echo "WorkSpace Creado!"
                    Start-Sleep -s 10
                    Invoke-RestMethod -Uri https://schematics.cloud.ibm.com/v1/workspaces/$id/plan -Method "Post" -Headers @{"Authorization" = $token ; "refresh_token" = $token}
                    echo "Plan generado!"
                    '''
                    
                    /* Start-Sleep -s 40
                    Invoke-RestMethod -Uri https://schematics.cloud.ibm.com/v1/workspaces/$id/apply -Method "Put" -Headers @{"Authorization" = $token ; "refresh_token" = $token}
                    echo "Plan aplicado!" 
                    Invoke-RestMethod -Uri https://schematics.cloud.ibm.com/v1/workspaces/$id/destroy -Method "Put" -Headers @{"Authorization" = $token ; "refresh_token" = $token}
                    echo "Plan destruido!" */
                
                }
                }
            }
        }
    }
}
