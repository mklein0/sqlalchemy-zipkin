#################
SQLAlchemy-Zipkin
#################

An zipkin extension for SQLAlchemy library based on py\_zipkin.


************
Installation
************

.. code-block:: bash

  pip install SQLAlchemy-Zipkin


*****
Usage
*****

.. code-block:: python

  import requests
  import sqlalchemy_zipkin


  PREAMBLE = sqlalchemy_zipkin.ZIPKIN_THRIFT_PREAMBLE


  def http_transport(encoded_span):
      # type: (bytes) -> None

      # The collector expects a thrift-encoded list of spans. Instead of
      # decoding and re-encoding the already thrift-encoded message, we can just
      # add header bytes that specify that what follows is a list of length 1.
      url = 'http://zipkin:9411/api/v1/spans'

      body = PREAMBLE + encoded_span
      requests.post(
          url,
          data=body,
          headers={'Content-Type': 'application/x-thrift'},
      )


   sqla_instance = sqlalchemy_zipkin.SqlAlchemyZipkinInstrumentation(
       http_transport, sample_rate=50.0)
   sqla_instance.start()


*********
Reference
*********

  * http://documentation-style-guide-sphinx.readthedocs.io/en/latest/style-guide.html
