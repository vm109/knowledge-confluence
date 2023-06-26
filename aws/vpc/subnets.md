# AWS VPC - Subnetting
<br/>

## what are subnets in a vpc?
- subnet is ip address subdivision of vpc.
- 1 subnet -> 1 availability zone.
- subnets isolates resources withing a vpc.
- subnets has private subnet and public subnet.

## practical subnetting
### public subnet
- create a vpc with CIDR range. `example: 10.0.0.0/24`
- To create subnet it has to be in VPC CIDR range
- so chose a subnet with CIDR. `example: 10.0.0.0/28`

```
If we place a ec2 instance within this subnet we cannot reach the instance `yet`
```
- create a gateway to connect VPC to internet [ similar to home network gateway ]
- route tables allow a subnet to connect to internet gateway.
- associate a subnet to internetgateway through route table to make it public subnet.