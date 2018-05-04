### DCL - DATA CONTROL LANGUAGE

<p>

Q.1 Create a user and permissions?
	
	* create user batch identified by psw;

	* drop user batch;
	
	* grant createsession to batch; 

	* grant unlimited tablespace to batch; // tablespace and tablesession permissions are permitted.

	* grant create any table to batch;

	* revoke create any table from batch;