<script lang="ts">
    import BuyNowModal from './BuyNowModal.svelte';
    import { ethers } from 'ethers';

    let showModal = false;
    let connectedAccount: string;

    function onOpenChange() {
        showModal = !showModal;
    }

    const provider = new ethers.providers.Web3Provider(window.ethereum);

    async function connectWallet() {
        if (window.ethereum) {
            try {
                await window.ethereum.request({ method: 'eth_requestAccounts' });
                const signer = provider.getSigner();
                connectedAccount = await signer.getAddress();
            } catch (e) {
                console.log(e);
            }
        } else {
            alert('You need to install a browser wallett');
        }
    }
</script>

<button class="text-red" on:click={onOpenChange}>Show Modal</button>

<BuyNowModal
    isOpen={showModal}
    contractAddress={'0x4b15a9c28034dc83db40cd810001427d3bd7163d'}
    tokenId={'12821'}
    {onOpenChange}
    {connectWallet}
    {connectedAccount}
/>
