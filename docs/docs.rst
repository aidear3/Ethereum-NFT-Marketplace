=====
Ethereum Marketplace Document
=====

.. code-block:: solidity

  interface IMarketplace {
     struct SellOrder {
        address seller;
        address token;
        address contractAddr;
        uint256 nftId;
        address buyer;
        uint256 price;
        uint256 startedAt;
        uint256 endedAt;
        bool isCanceled;
        bool isEnded;
    }
    
    struct Bid {
        address bidder;
        address token;
        address nftOwner;
        uint256 sellOrderId;
        uint256 price;
        uint256 biddedAt;
        uint256 bidEndedAt;
        bool isCanceled;
        bool isEnded;
    }
    
    function createSellOrder(
      address _contractAddr,
      uint256 _nftId,
      address _token,
      uint256 _price
    ) external;
    
    function createBid(
      uint256 _orderId,
      address _token,
      uint256 _price
    ) external;
    
    function acceptBid(
      uin256 _bidId,
      uint256 _orderId
    ) external;
    
    function cancelBid(uint256 _bidId) external;
    
    function cancelSellOrder(uint256 _orderId) external;
    
    function createERC721Contract(
      string calldata _collectionName,
      string calldata _collectionSymbol,
      string calldata _collectionDescription,
      address _factory
    ) external;
    
    function sellOrder(uint256 _sellOrderId) external view returns(SellOrder memory);
    
    function bid(uint256 _bidId) external view returns(Bid memory);
    
    function getUserContract(address _user) external view returns(address);
  }

---------------------------------------------------------------------------------------------

create sell order
===================

.. code-block:: solidity

   function createSellOrder(
      address _contractAddr,
      uint256 _nftId,
      address _token,
      uint256 _price
    ) external;
    
Will create a sell order.

----------
Parameters
----------

1. ``_contractAddr`` - ``address``: The sell order creator nft's contract address.
2. ``_nftId`` - ``uint256``: The nft's id which user is going to sell it.
3. ``_token`` - ``address``: The address of token (currency like USDC, ...) that user wishes to make a price for his/her sell order
4. ``_price`` - ``uint256``: The price of the sell order in decimal format.

.. warning:: User must approve the marketplace to access the nft token to list it in the market.

---------------------------------------------------------------------------------------------

create bid
===================

.. code-block:: solidity

   function createBid(
      uint256 _orderId,
      address _token,
      uint256 _price
    ) external;
    
Will create a bid for listed nft.

.. warning:: User must approve marketplace to access the ``_price`` amount of the ``_token`` to create the bid.

----------
Parameters
----------

1. ``_orderId`` - ``uint256``: The id of the sell order that bidder wishes to make a bid for it.
2. ``_token`` - ``address``: The address of the token which bidder wishes to pay the nft in that.
3. ``_price`` - ``uint256``: The amount of token ``_token`` that bidder wishes to pay in decimal.

.. warning:: The ``_token`` must be one of the accepted tokens in the marketplace smart contract.

---------------------------------------------------------------------------------------------

accept bid
==================

.. code-block:: solidity

    function acceptBid(
      uin256 _bidId,
      uint256 _orderId
    ) external;
    
Sell order owner will accept a relevant bid by calling this function.

----------
Parameters
----------

1. ``_bidId`` - ``uint256``: The bid id which sell order owner wishes to accept it.
2. ``_orderId`` - ``uint256``: The order id of the sell order owner.

---------------------------------------------------------------------------------------------

