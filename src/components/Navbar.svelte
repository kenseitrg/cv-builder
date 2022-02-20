<script lang="ts">
    import {
        Collapse,
        Navbar,
        NavbarToggler,
        NavbarBrand,
        Nav,
        NavItem,
        NavLink,
        Dropdown,
        DropdownToggle,
        DropdownMenu,
        DropdownItem,
        Button,
    } from "sveltestrap";

    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    let isOpen = false;

    function handleUpdate(event) {
        isOpen = event.detail.isOpen;
    }

    const handleClick = (event) => {
        event.preventDefault();
        dispatch("savepdf-clicked", event);
    };
</script>

<Navbar color="light" light expand="md" class="mb-3">
    <NavbarBrand href="/">CV Builder</NavbarBrand>
    <NavbarToggler on:click={() => (isOpen = !isOpen)} />
    <Collapse {isOpen} navbar expand="md" on:update={handleUpdate}>
        <Nav class="ms-auto" navbar>
            <NavItem>
                <Button outline on:click={handleClick}>Save PDF</Button>
            </NavItem>
        </Nav>
    </Collapse>
</Navbar>
