# Azure-oss-hand-on-lab

## 리소스 그룹 생성
```
az group create --name user20OsTicketPaaSRG --location "West US"
```

## 데이터베이스 생성(PaaS형 MySQL DB)
```
az mysql server create --resource-group user20OsTicketPaaSRG --name user20osticketsrv01 --location "West US" --admin-user demouser --admin-password demo@pass123 --sku-name B_Gen5_2 --storage-size 51200 --ssl-enforcement Disabled
```

## MySQL접근 권한설정
```
az mysql server firewall-rule create --resource-group user20OsTicketPaaSRG --server-name user20osticketsrv01 --name Internet --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## DB접속 문자열
```
Database=osTicket; Data Source=user20osticketsrv01.mysql.database.azure.com; User Id=demouser@user20osticketsrv01; Password=demo@pass123
```
## 웹앱 만들기 - AppService Plan 생성
```
az appservice plan create -n OsTicket -g user20OsTicketPaaSRG --is-linux -l "West US" --sku S1 --number-of-workers 1
```

## 웹앱 생성
```
az webapp create -n user20osTicketsystem -g user20OsTicketPaaSRG -p OsTicket -r "php|7.4"
```
