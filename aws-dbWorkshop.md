2017, February 21
**AMAZON RDS**

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


**AURORA**
		
		* what is aurora?
			- open source compatible relational db
			- re-imagined relational db (cloud optimized)
				- scale-out and distributed design
					- purpose-built log-structured distrubtuted storage system designed for dbs
					- storeage volume is striped across hundreds of stroage nodes distrubuted over 3 diff availability zones
					- 6 copies of data, 2 copies in each availability zone to protect against AZ+1 failures
				- service-oriented architecture leveraging AWS 
				- RDS: automate administrative tasks
		* scaling with instance sizes
			- scales with instance size for both read and write
			- do less work; be more efficient
				- fewer IOs, minimized network packets, cache prior results, offload the db engine
				- process async, reduce latency path, use lock-free data stuctures, batch operations together
			- async group commits
				- request I/O with first write, fill buffer til write picked up
				- individual write durable when 4 of 6 storge nodes ACK
			- adaptive thread pool
				- re-entrant connections multiplexed to active threads
				- kemel-space epoll() inserts into latch-free event queue
				- dynamically sizes threads pool
			- aurora lock management
				- same lock semantics as MySQL
				- concurrent access to lock chains

		* new things
			- cached read performance  
				- catalog concurrency - improve data dictionary synchronization and cache eviction
				- NUMA aware scheduler
				- read views
			- non-cached read performance
				- smart scheduler - now dynamically assigns threads b/t IO heavy and CPU heavy workloads
				- smart selector
				- logical read ahead (LRA)
			- hot row contention
				- highly contended workloads had high memory and CPU
			- insert performance
				- accelerates batch inserts sorted by primary keys
			- faster index build
				- bulds leaf blocks and then the branches of the tree
			- spatial indexes
				- z-index (dimensionally ordered space filling curve)
			- storage durability
				- storage volume automatically grows up to 64TB
			- more replicas
				- aurora cluster contains primary node and up to 15 replicas
				- failing db nodes are automatically detected and replaced
			- continuous backup
			- instance crash recovery
				- underlying storage replays redo records on demand as part of a disk read
				- parallel, distributed, async
				- no replay for startup
			- survivable caches
				- moved cache out of the db process
				- cache remains warm in the event of db restart
				- lets you resume fully loaded operations faster
			- faster failover
			- aurora with PostgreSQL compatibility now in preview


**DB MIGRATION**

		* migration options
			- use native tools if you're not switching engines and can take downtime
		* what are DMS and SCT?
			- AWS database migration service easily and securely migrate and/or replace you dbs and data warehouses to AWS
			- AWS schema conversion tool converts your commercial db and data warehouse schemas to open-source engines or AWS native services, such as Aurora and Redshift
		* when to use
			- modernize, migrate, replicate
		* new SCT data extractors
			- extract data from your data warehouse through local migration agents
			- data optimized for Redshift and saved in local files
			- files loaded to an Amazon S3 bucket and then to Redshift

