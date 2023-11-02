# validated-security-findings

## <a id='H-02'></a>H-02. The setPassword Function is lacking access control            

### Relevant GitHub Links
	
https://github.com/Cyfrin/2023-10-PasswordStore/blob/main/src/PasswordStore.sol#L26

## Summary
The setPassword Function is lacking access control

## Vulnerability Details
The setPassword function is supposed to be used to set the password of the contract however it lacks an access control protection which means that anyone will be able to set the password of the contract.

## Impact
anyone will be able to set the password and  access the contract therefore there the contract is compromised

## Tools Used
manual analysis

## Recommendations

consider adding a modifier for access control so that only the owner of this contract will be able to set the password of this contract as below.

```solidity
modifier onlyOwner() {
    require(msg.sender == s_owner, "Stop you are not the owner");
    _;
}
```

then you can now protect our function from malicious users  as below

```solidity
function setPassword(string memory newPassword) external onlyOwner {
 if (msg.sender != s_owner) {
            revert PasswordStore__NotOwner();
        }
    s_password = newPassword;
    emit SetNetPassword(newPassword);
}
```
		
