# graylog-adfs
ADFS Content Pack for Graylog. Based on ADFS 3.0 (Windows 2012 R2)

## Contains ##
* an input for ADFS event logs
* a set of extractors for some events
* a simple dashboard

## nxlog fowarder configuration ##

	## AD FS logs to the right collector

	<Input in>
	    Module      im_msvistalog
		Exec        if ($SourceName !~ /^AD FS/) drop();
	</Input>

	<Output out>
	    Module      om_udp
	    Host        your-graylog-server.youdomain.here
	    Port        5001
	    OutputType  GELF
	</Output>

	<Route 1>
	    Path        in => out
	</Route>


## INSTALL ##

You must perform two search and replace before importing the JSON file in Graylog:
- CONTOSO.COM by your full domain name
- CONTOSO by your short domain name
That is because user may log in with UPN or not and the logs do not standardize the login representation.
