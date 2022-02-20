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
    } from "sveltestrap";

    import { createEventDispatcher } from "svelte";

    export let profile = "";
    const dispatch = createEventDispatcher();

    const handleChange = (event) => {
        event.preventDefault();
        dispatch("profile-changed", profile);
    };
</script>

<Card class="mb-1">
    <CardHeader>
        <Container fluid>
            <Row>
                <Col>
                    <p>Profile</p>
                </Col>
                <Col xs="auto">
                    <Button outline id="togglerProf">
                        <Icon name="three-dots" />
                    </Button>
                </Col>
            </Row>
        </Container>
    </CardHeader>
    <Collapse toggler="#togglerProf">
        <CardBody>
            <Container fluid>
                <Row>
                    <Col>
                        <Label for="profileInfo">Profile</Label>
                        <Input
                            type="textarea"
                            name="profileInfo"
                            id="profileInfo"
                            placeholder="Your personal information"
                            bind:value={profile}
                            on:change={handleChange}
                        />
                    </Col>
                </Row>
            </Container>
        </CardBody>
    </Collapse>
</Card>
