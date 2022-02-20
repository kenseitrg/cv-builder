<script>
    import {
        Card,
        CardBody,
        CardHeader,
        Col,
        Container,
        Input,
        Label,
        Row,
        Button,
        Collapse,
        Icon,
        InputGroup,
        InputGroupText,
    } from "sveltestrap";

    import { createEventDispatcher } from "svelte";

    export let contacts = {
        email: "",
        phone: "",
        adress: "",
    };

    const dispatch = createEventDispatcher();

    const handleChange = (event) => {
        event.preventDefault();
        contacts = contacts;
        dispatch("contacts-changed", contacts);
    };
</script>

<Card class="mb-1">
    <CardHeader>
        <Container fluid>
            <Row>
                <Col>
                    <p>Contacts</p>
                </Col>
                <Col xs="auto">
                    <Button outline id="togglerCont">
                        <Icon name="three-dots" />
                    </Button>
                </Col>
            </Row>
        </Container>
    </CardHeader>
    <Collapse toggler="#togglerCont">
        <CardBody>
            <Container fluid>
                <Row>
                    <Col>
                        <Label for="userEMail">Email</Label>
                        <Input
                            type="email"
                            name="userEMail"
                            id="userEMail"
                            placeholder="mail@example.com"
                            bind:value={contacts.email}
                            on:change={handleChange}
                        />
                    </Col>
                </Row>
                <Row>
                    <Col>
                        <Label for="userPhone">Phone number</Label>
                        <Input
                            type="tel"
                            name="userPhone"
                            id="userPhone"
                            placeholder="+1 111 111 11 11"
                            bind:value={contacts.phone}
                            on:change={handleChange}
                        />
                    </Col>
                </Row>
                <Row>
                    <Col>
                        <Label for="userAdress">Adress</Label>
                        <Input
                            type="text"
                            name="userAdress"
                            id="userAdress"
                            placeholder="Brooklyn, NY 11222"
                            bind:value={contacts.adress}
                            on:change={handleChange}
                        />
                    </Col>
                </Row>
            </Container>
        </CardBody>
    </Collapse>
</Card>
