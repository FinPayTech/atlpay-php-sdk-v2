Refunds
=======

To refund a payment, you create a ``Refund`` object. You can retrieve and process partial or full refund. Refunds are identified by a unique, random ID.

API Endpoint : ``https://api.atlpay.com/v2/charges/refund``

The refund object
-----------------
.. csv-table::
   :header: "Attribute", "Description"
   :widths: 20, 80

   "type", "type of the object, in this case it will return ``refund``"
   "id", "Unique identifier for the object."
   "currency", "Three-letter ISO currency code, in lowercase."
   "amount", "A positive integer in the smallest currency unit (e.g., 100 to charge £1.00) representing refund amount."
   "fee_refunded", "The fee refunded (if any)"
   "status", "Status of the refund"
   "created", "Time at which the object was created. Measured in seconds since the Unix epoch."
   "mode", "``live`` if the object exists in live mode or the value ``test`` if the object exists in test mode."


Create a refund
---------------

To refund a charge, you create a Refund object. If your API key is in test mode, then charge won't actually be refunded, although everything else will occur as if in live mode. (ATLPay assumes that the refund would have completed successfully).

.. csv-table::
   :header: "Attribute", "Mandatory", "Description"
   :widths: 20, 20, 60

   "amount", "No", "A positive integer in the smallest currency unit (e.g., 100 to charge £1.00) representing how much to refund. If not provided the full amount or remaining balance will be refunded"

**Returns**

Returns a Charge object if the charge succeeded. Returns an error if something goes wrong. A common source of error is refunding an already refunded charge.

Example request

.. code-block:: bash

    curl -X POST \
      https://api.atlpay.com/v2/charges/refund/{CHARGE-ID-HERE} \
      -H 'X-Api-Key: YOUR_API_KEY' \
      -F amount=500 \


Example response

.. code-block:: json

    {
        "type": "refund",
        "id": "978dfd87-13b8-443a-892e-fca0380ef7d4",
        "amount": 500,
        "currency": "GBP",
        "fee_refunded": 0,
        "status": "REFUNDED",
        "created": "2020-04-08T11:55:21",
        "mode": "test"
    }

Retrieve a refund
-----------------

Retrieves the details of a refund that has previously been created. Supply the unique charge ID that was returned from your previous request, and ATLPay will return the corresponding refund information. The same information is returned when creating a refund.

Example request

.. code-block:: bash

    curl -X GET \
    	https://api.atlpay.com/v2/charges/refund/978dfd87-13b8-443a-892e-fca0380ef7d4 \
    	-H 'X-Api-Key: YOUR_API_KEY'

Example response

.. code-block:: json

   {
        "type": "refund",
        "id": "978dfd87-13b8-443a-892e-fca0380ef7d4",
        "amount": 500,
        "currency": "GBP",
        "fee_refunded": 0,
        "status": "REFUNDED",
        "created": "2020-04-08T11:55:21",
        "mode": "test"
    }