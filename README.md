contract SimpleToken {
    // Event emitted when tokens are transferred
    event Transfer(address indexed _from, address indexed _to, uint256 _value);

    // Mapping to store balances of each address
    mapping(address => uint256) public balances;

    // Total supply of tokens
    uint256 public totalSupply;

    // The address that deployed the contract (owner)
    address public owner;

    // Constructor: Deploys the contract and mints initial supply to the deployer
    constructor(uint256 initialSupply) {
        totalSupply = initialSupply;
        balances[msg.sender] = initialSupply; // Assign all initial supply to the deployer
        owner = msg.sender;
    }

    // Function to transfer tokens from the sender's balance to a recipient's balance
    function transfer(address _to, uint256 _value) public returns (bool success) {
        // Require that the sender has enough balance
        require(balances[msg.sender] >= _value, "Insufficient balance");
        // Require that the recipient is not the zero address
        require(_to != address(0), "Cannot send to zero address");

        // Subtract value from sender's balance
        balances[msg.sender] -= _value;
        // Add value to recipient's balance
        balances[_to] += _value;

        // Emit a Transfer event
        emit Transfer(msg.sender, _to, _value);

        return true;
    }

    // Function to check the balance of an address
    function balanceOf(address _owner) public view returns (uint256 balance) {
        return balances[_owner];
    }
}
