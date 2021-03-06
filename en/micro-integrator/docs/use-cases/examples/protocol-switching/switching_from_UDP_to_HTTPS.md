# Switching from UDP to HTTP/S

This example demonstrates how WSO2 Micro Integrator receives SOAP messages over UDP and forwards them over HTTP.

## Synapse configuration

Following are the integration artifacts (proxy service) that we can used to implement this scenario. See the instructions on how to [build and run](#build-and-run) this example.

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<proxy name="StockQuoteProxy" startOnLoad="true" transports="udp" xmlns="http://ws.apache.org/ns/synapse">
    <target>
        <inSequence>
            <log level="full"/>
            <property name="OUT_ONLY" value="true"/>
            <send>
                <endpoint>
                    <address uri="http://localhost:9000/services/SimpleStockQuoteService"/>
                </endpoint>
            </send>
        </inSequence>
    </target>
    <publishWSDL key="conf:UDP_WSDL/sample_proxy_1.wsdl" preservePolicy="true"/>
    <parameter name="transport.udp.port">9999</parameter>
    <parameter name="transport.udp.contentType">text/xml</parameter>
</proxy>
```

## Build and Run

Create the artifacts:

1. [Set up WSO2 Integration Studio](../../../../develop/installing-WSO2-Integration-Studio).
2. [Create an integration project](../../../../develop/create-integration-project) with an <b>ESB Configs</b> module and an <b>Composite Exporter</b>.
3. Add [sample_proxy_1.wsdl](https://github.com/wso2-docs/WSO2_EI/blob/master/samples-protocol-switching/sample_proxy_1.wsdl) as a [registry resource](../../../../develop/creating-artifacts/creating-registry-resources) (change the registry path of the proxy accordingly). 
4. Create the [proxy service](../../../../develop/creating-artifacts/creating-a-proxy-service) with the configurations given above.
5. [Deploy the artifacts](../../../../develop/deploy-artifacts) in your Micro Integrator.

Set up the back-end service:

* Download the [stockquote_service.jar](
https://github.com/wso2-docs/WSO2_EI/blob/master/Back-End-Service/stockquote_service.jar)

* Run the mock service using the following command
    ```bash
    java -jar stockquote_service.jar
    ```

[Enable the UDP transport](../../../../setup/transport_configurations/configuring-transports/#configuring-the-udp-transport) and start the Micro-Integrator.

Send the following message via UDP to the UDP listener port (9999).
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Header xmlns:wsa="http://www.w3.org/2005/08/addressing">
        <wsa:To>udp://localhost:9999/services/StockQuoteProxy</wsa:To>
        <wsa:ReplyTo>
            <wsa:Address>http://www.w3.org/2005/08/addressing/none</wsa:Address>
        </wsa:ReplyTo>
        <wsa:MessageID>urn:uuid:464d2e2a-cd47-4c63-a7c6-550c282a1e3c</wsa:MessageID>
        <wsa:Action>urn:placeOrder</wsa:Action>
    </soapenv:Header>
    <soapenv:Body>
        <m0:placeOrder xmlns:m0="http://services.samples">
            <m0:order>
                <m0:price>172.23182849731984</m0:price>
                <m0:quantity>18398</m0:quantity>
                <m0:symbol>IBM</m0:symbol>
            </m0:order>
        </m0:placeOrder>
    </soapenv:Body>
</soapenv:Envelope>
``` 
In linux, we can save the above request in a <strong>request.xml</strong> file and use netcat to send the UDP request. 

```bash
nc -u localhost 9999 < request.xml
```
