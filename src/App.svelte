<script>
	import { Row, Col, Container, Styles } from "sveltestrap";
	import MainForm from "./components/MainForm.svelte";
	import Navbar from "./components/Navbar.svelte";
	import Preview from "./components/Preview.svelte";
	import { jsPDF } from "jspdf";
	import html2canvas from "html2canvas";

	let cvInfo = {
		bio: {
			firstName: "Your",
			lastName: "Name",
			title: "Title",
		},
		contacts: {
			email: "example@example.com",
			phone: "+1 111 111 11 11",
			adress: "Brooklyn, NY 11222",
		},
		profile: "Very experienced guy",
		education: [
			{
				start: "01-01-2001",
				end: "01-01-2005",
				place: "University of Life",
				degree: "B.Sc. in Sleeping",
			},
		],
		experience: [
			{
				start: "01-01-2001",
				end: "01-01-2005",
				place: "ACME Inc.",
				description: "Pillow checker",
			},
		],
	};

	const handleChange = (event) => {
		event.preventDefault();
		cvInfo = event.detail;
	};

	const handleSave = (event) => {
		event.preventDefault();

		const html = document.getElementById("preview");
		html2canvas(html).then((canvas) => {
			const imgData = canvas.toDataURL("image/png");
			const pdf = new jsPDF({
				orientation: "p",
				unit: "mm",
				format: "a4",
				putOnlyUsedFonts: true,
				floatPrecision: 16,
			});
			const imgProps = pdf.getImageProperties(imgData);
			const pdfWidth = pdf.internal.pageSize.getWidth();
			const pdfHeight = (imgProps.height * pdfWidth) / imgProps.width;
			pdf.addImage(imgData, "PNG", 0, 0, pdfWidth, pdfHeight);
			pdf.save("CV.pdf");
		});
		/*doc.html(html, {
			callback: function (doc) {
				doc.save("CV.pdf");
			},
			x: 0,
			y: 0,
		});*/
	};
</script>

<Styles />

<header>
	<Navbar on:savepdf-clicked={handleSave} />
</header>

<main>
	<Container fluid>
		<Row cols={2}>
			<Col><MainForm on:form-changed={handleChange} /></Col>
			<Col>
				<div id="preview">
					<Preview {cvInfo} />
				</div>
			</Col>
		</Row>
	</Container>
</main>
