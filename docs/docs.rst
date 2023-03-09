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

create sell order
=====
