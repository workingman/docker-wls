FROM workingman/jre:8

ENV ORACLE_HOME=/u01/oracle \
    USER_MEM_ARGS="-Djava.security.egd=file:/dev/./urandom" \
    PATH=$PATH:/usr/java/default/bin:/u01/oracle/oracle_common/common/bin \
    FMW_PKG=fmw_12.2.1.0.0_wls_quick_Disk1_1of1.zip \
    FMW_JAR=fmw_12.2.1.0.0_wls_quick.jar \
    DEBUG_FLAG=true\
    PRODUCTION_MODE=dev
   
RUN mkdir -p /u01 && \
    chmod a+xr /u01 && \
    useradd -b /u01 -d /u01/oracle -m -s /bin/bash oracle && \
    chown oracle:oracle -R /u01

COPY $FMW_PKG install.file oraInst.loc /u01/

USER oracle

RUN cd /u01 && $JAVA_HOME/bin/jar xf /u01/$FMW_PKG && cd - && \
    $JAVA_HOME/bin/java -jar /u01/$FMW_JAR \
      -invPtrLoc /u01/oraInst.loc \
      -jreLoc $JAVA_HOME \
      -ignoreSysPrereqs \
      -force \
      -novalidation \
      ORACLE_HOME=$ORACLE_HOME && \
    rm /u01/$FMW_JAR /u01/$FMW_PKG /u01/oraInst.loc /u01/install.file

WORKDIR $ORACLE_HOME 

CMD ["bash"]
