#COMMAND: earthly -P --output --no-cache +parallel
#Parallel working
#VERSION --no-use-registry-for-with-docker 0.7
#Parallel not working
VERSION --use-visited-upfront-hash-collection 0.7

FROM earthly/dind:alpine

parallel:
    FOR num IN $(seq 5)
        COPY (+test-executor/TestResults --PROJECT=$num) ./TestResults
    END

    SAVE ARTIFACT ./TestResults testresults AS LOCAL earthly-artifacts/testresults
    
test-executor:
    ARG PROJECT
    ARG ID

    WITH DOCKER --pull hello-world
        RUN sleep 5 && mkdir TestResults && echo hello > ./TestResults/dummy_${PROJECT}.txt
    END
   
    SAVE ARTIFACT ./TestResults TestResults
