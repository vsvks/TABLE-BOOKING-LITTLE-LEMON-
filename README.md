# TABLE-BOOKING-LITTLE-LEMON-
table booking on emma johnson
import React from 'react';
import { Formik, Field, Form } from 'formik';
import * as Yup from 'yup';
import { Input, Button, FormControl, FormLabel, Box, Select, Textarea, useToast } from '@chakra-ui/react';

// Form validation schema using Yup
const reservationSchema = Yup.object({
  name: Yup.string().required('Name is required'),
  email: Yup.string().email('Invalid email address').required('Email is required'),
  phone: Yup.string().required('Phone number is required'),
  partySize: Yup.number().required('Please select a party size').min(1, 'Must be at least 1'),
  date: Yup.date().required('Date is required'),
  time: Yup.string().required('Time is required'),
  specialRequests: Yup.string(),
});

const ReserveTable = () => {
  const toast = useToast();

  const handleSubmit = (values) => {
    // Send reservation data to the server (this is a simulation)
    toast({
      title: 'Reservation confirmed',
      description: `Your table for ${values.partySize} people has been booked.`,
      status: 'success',
      duration: 5000,
      isClosable: true,
    });
  };

  return (
    <Box maxWidth="600px" margin="auto" padding="4">
      <Formik
        initialValues={{
          name: '',
          email: '',
          phone: '',
          partySize: 2,
          date: '',
          time: '',
          specialRequests: '',
        }}
        validationSchema={reservationSchema}
        onSubmit={handleSubmit}
      >
        {({ values, errors, touched }) => (
          <Form>
            <FormControl isInvalid={touched.name && errors.name}>
              <FormLabel htmlFor="name">Name</FormLabel>
              <Field
                as={Input}
                id="name"
                name="name"
                placeholder="Your name"
              />
            </FormControl>

            <FormControl isInvalid={touched.email && errors.email}>
              <FormLabel htmlFor="email">Email</FormLabel>
              <Field
                as={Input}
                id="email"
                name="email"
                type="email"
                placeholder="Your email"
              />
            </FormControl>

            <FormControl isInvalid={touched.phone && errors.phone}>
              <FormLabel htmlFor="phone">Phone Number</FormLabel>
              <Field
                as={Input}
                id="phone"
                name="phone"
                type="text"
                placeholder="Your phone number"
              />
            </FormControl>

            <FormControl isInvalid={touched.partySize && errors.partySize}>
              <FormLabel htmlFor="partySize">Party Size</FormLabel>
              <Field as={Select} id="partySize" name="partySize">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
                <option value="6">6</option>
                <option value="7">7</option>
                <option value="8">8</option>
              </Field>
            </FormControl>

            <FormControl isInvalid={touched.date && errors.date}>
              <FormLabel htmlFor="date">Date</FormLabel>
              <Field
                as={Input}
                id="date"
                name="date"
                type="date"
              />
            </FormControl>

            <FormControl isInvalid={touched.time && errors.time}>
              <FormLabel htmlFor="time">Time</FormLabel>
              <Field
                as={Select}
                id="time"
                name="time"
              >
                <option value="18:00">6:00 PM</option>
                <option value="19:00">7:00 PM</option>
                <option value="20:00">8:00 PM</option>
              </Field>
            </FormControl>

            <FormControl>
              <FormLabel htmlFor="specialRequests">Special Requests</FormLabel>
              <Field
                as={Textarea}
                id="specialRequests"
                name="specialRequests"
                placeholder="Any special requests?"
              />
            </FormControl>

            <Button type="submit" colorScheme="teal" width="full" marginTop="4">
              Reserve a Table
            </Button>
          </Form>
        )}
      </Formik>
    </Box>
  );
};

export default ReserveTable;
import React from 'react';
import { ChakraProvider } from '@chakra-ui/react';
import ReserveTable from './ReserveTable';

function App() {
  return (
    <ChakraProvider>
      <div className="App">
        <h1>Little Lemon Restaurant</h1>
        <ReserveTable />
      </div>
    </ChakraProvider>
  );
}

export default App;

