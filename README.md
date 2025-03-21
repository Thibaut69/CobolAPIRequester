<h1>Sub-programs</h1>
These sub-programs are made available as is, and allow you to send at least GET or POST API calls.
They are provided without any guarantee.

<h1>Compilation JCL</h1>
XAPIRC can be compile as any Cobol CICS program.

XAPIRB need some specific compile option like NODYN param to be compiled with static programs.
Its JCL is provided in the first lines of the member SYS1.SAMPLIB(HWTHXCB1)
I provide the COMPXAPI JCL, which use the PROC IGYWCL to compile XAPIRB.

<h1>Call samples</h1>

<h2>To perform a call in a Cobol batch</h2>

           MOVE "POST"                   TO W-METHOD.
           MOVE "https://mydomain.com"   TO W-URI.
           MOVE 443                      TO W-PORT.
           MOVE "/myservicetocall"       TO W-SERVICE.
           MOVE "application/json"       TO W-MEDIA.

           MOVE SPACES     TO W-USER.
           MOVE SPACES     TO W-PASSWORD.
           MOVE ZEROES     TO W-CONTENT-LENGTH.

           STRING W-TYPE-TOKEN DELIMITED BY SIZE
                  " " DELIMITED BY SIZE
                  W-ACCESS-TOKEN DELIMITED BY SIZE
           INTO W-HEADER-AUTH.
           
           MOVE "mykeyring"   TO W-KEYRING.
           MOVE "N"           TO W-DEBUG-MODE.

           MOVE ZEROES        TO W-HTTP-RETURN-CODE.
           MOVE SPACES        TO W-REPONSE.

           OPEN OUTPUT INFILE.

           MOVE WS-DATA TO INFILE-RECORD.

           WRITE INFILE-RECORD.

           CLOSE INFILE.

           MOVE    'XAPIRB' TO W-PGM.
           CALL     W-PGM USING W-COMMAREA.


  <h2> To perform a call in a Cobol CICS </h2>

           MOVE "POST"              TO W-METHOD.
           MOVE "HTTPS"             TO W-SCHEME.
           MOVE "mydomain.com"      TO W-URI.
           MOVE 443                 TO W-PORT.
           MOVE "/myservice"        TO W-SERVICE.
           MOVE "application/json"  TO W-MEDIA.
           MOVE WS-DATA             TO W-MESSAGE.
           MOVE SPACES              TO W-USER.
           MOVE SPACES              TO W-PASSWORD.
           STRING W-TYPE-TOKEN DELIMITED BY SIZE
                  " " DELIMITED BY SIZE
                  W-ACCESS-TOKEN DELIMITED BY SIZE
           INTO W-AUTH

           MOVE        'XAPIRC' TO W-PGM
           CALL        W-PGM USING W-COMMAREA.
