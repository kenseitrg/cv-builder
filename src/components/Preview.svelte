<script>
    import {
        Card,
        CardBody,
        CardHeader,
        Col,
        Container,
        Row,
        Table,
    } from "sveltestrap";

    export let cvInfo = {};
</script>

<Container fluid class="border">
    <Row class="mb-1">
        <Col>
            <h1>{cvInfo.bio.firstName} {cvInfo.bio.lastName}</h1>
            <h2 class="text-muted">{cvInfo.bio.title}</h2>
        </Col>
    </Row>
    <Row class="mb-1">
        <Card>
            <CardHeader>Contacts</CardHeader>
            <CardBody>
                <Row>
                    <Col>email: {cvInfo.contacts.email}</Col>
                    <Col>phone: {cvInfo.contacts.phone}</Col>
                    <Col>adress: {cvInfo.contacts.adress}</Col>
                </Row>
            </CardBody>
        </Card>
    </Row>
    <Row class="mb-1">
        <Card>
            <CardHeader>Profile</CardHeader>
            <CardBody>
                <Row>
                    <p>{cvInfo.profile}</p>
                </Row>
            </CardBody>
        </Card>
    </Row>
    <Row class="mb-1">
        <Card>
            <CardHeader>Education</CardHeader>
            <CardBody>
                <Table hover borderless>
                    <thead>
                        <tr>
                            <th>Start</th>
                            <th>End</th>
                            <th>Place</th>
                            <th>Degree</th>
                        </tr>
                    </thead>
                    <tbody>
                        {#each cvInfo.education as edu}
                            <tr>
                                <td>{edu.start}</td>
                                <td>{edu.end}</td>
                                <td>{edu.place}</td>
                                <td>{edu.degree}</td>
                            </tr>
                        {/each}
                    </tbody>
                </Table>
            </CardBody>
        </Card>
    </Row>
    <Row class="mb-1">
        <Card>
            <CardHeader>Experience</CardHeader>
            <CardBody>
                <Table hover borderless>
                    <thead>
                        <tr>
                            <th>Start</th>
                            <th>End</th>
                            <th>Place</th>
                            <th>Job Details</th>
                        </tr>
                    </thead>
                    <tbody>
                        {#each cvInfo.experience as job}
                            <tr>
                                <td>{job.start}</td>
                                <td>{job.end}</td>
                                <td>{job.place}</td>
                                <td>{job.description}</td>
                            </tr>
                        {/each}
                    </tbody>
                </Table>
            </CardBody>
        </Card>
    </Row>
</Container>
