**AMAZON RDS**
2017, February 21

	* multi-engine support
	* automated provisioning, scaling, patching, backup/restore
			- naturally grow over time
			- control costs (flexible to scale up or down as needed)
			- handle higher load or lower usage
	* read replicas
			- bring data close to customer's apps in different regions
			- relieve pressure on master node for supporting reads and writes
			- promote to a master db for faster recovery in event of disaster
	* to counter replication lag: RDS provides enterprise-grade fault tolerance for syncronous replication and automatic failover
	* security & compliance
			- network isolation
			- security groups
					- db instance IP firewall protection
			- AWS IAM based resource-lvl permission controls
					- AWS Identity and Access Management (IAM) to control who can perform actions on RDS
			- at rest encryption for all RDS engines AWS Key Manangement Service (KMS)
					- two-tiered key hierarchy using envelope encryption:
						- unique data key encrypts customer data
						- AWS KMS master keys encrypt data keys
			- Amazon VPC (virtual private cloud)
					- securely control network configuration
					- can setup db in subnet
	* AWS db migration service
			- fully manage service for migration from on-premises to the AWS Cloud with minimal downtime
			- migrates data to and from widely used commerical and open source dbs
			- schema conversion tool that converts source db schemas, stored procedures and application code to a different target format 
			- supports homogenous and heterogeneous data replications
			- TB-sized db can be migrated for as little as $3
